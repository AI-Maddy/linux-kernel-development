# :material-bug-check: Debugging Tools

Kernel bugs are harder to chase than user-space bugs — there's no libc to fall back on, and a crash can take the whole machine down with it.

Kernel bugs are harder to chase than user-space bugs: there is no libc to fall back on, a crash can take down the whole machine, and stack traces are not always symbolized by default. These tools cover most day-to-day needs.

## :material-console-line: printk and dynamic debug

!!! info "printk()"
    printk() remains the most common debugging tool. Messages go to the kernel ring buffer and can be read with dmesg.

!!! success "Dynamic debug"
    Rather than sprinkling permanent printk calls, use dynamic debug to enable verbose logging at runtime for specific files or functions.

```bash
echo 'file drivers/net/ethernet/example.c +p' > /sys/kernel/debug/dynamic_debug/control
```

## :material-chart-timeline: ftrace

ftrace traces function calls, scheduling events, and custom tracepoints with very low overhead, and is built into the kernel:

```bash
cd /sys/kernel/tracing
echo function > current_tracer
echo my_driver_probe > set_ftrace_filter
cat trace
```

## :material-bug: kgdb / kdb

!!! info "kgdb"
    For stepping through kernel code with a real debugger, kgdb connects a remote GDB session over serial or network to a target kernel built with CONFIG_KGDB.

!!! info "kdb"
    kdb provides a lighter-weight, built-in shell for inspecting state without a host machine.

## :material-file-search: Crash analysis

!!! success "Decoding a stack trace"
    When a kernel oopses, the printed stack trace can be resolved to file/line information with scripts/decode_stacktrace.sh, given a kernel build with debug symbols.

!!! success "Catch bugs before they crash"
    For reproducible crashes, KASAN (CONFIG_KASAN) and lockdep (CONFIG_PROVE_LOCKING) catch entire classes of memory-safety and locking bugs long before they cause a hard-to-diagnose crash.

## :material-alert: Pitfalls

!!! warning "Reaching for kgdb too early"
    Attaching a live debugger before trying printk/dynamic debug or ftrace wastes time on problems that logging alone would have shown.

!!! warning "Leaving KASAN and lockdep off in development"
    Skipping KASAN and lockdep in a development kernel lets memory-safety and locking bugs slip through until they cause a much harder-to-diagnose crash later.

## :material-help-circle: Self-Test

=== "Question 1"
    You suspect a timing or ordering issue between two kernel functions. Which tool should you reach for, and why?

=== "Answer 1"
    ftrace — it traces function calls and scheduling events with very low overhead, so you can see the actual call order and timing.

=== "Question 2"
    A kernel oopses and prints a raw stack trace. How do you turn it into file/line information?

=== "Answer 2"
    Run scripts/decode_stacktrace.sh against the oops output, using a kernel build that has debug symbols.

## :material-check-circle: Summary

- printk() plus dynamic debug gives a rough picture with the least setup.
- ftrace is the low-overhead way to see function calls, scheduling events, and tracepoints.
- kgdb (remote GDB) and kdb (built-in shell) are for inspecting live state logging can't capture.
- scripts/decode_stacktrace.sh turns a raw oops into file/line information.
- KASAN and lockdep, left enabled in a development kernel, catch many bugs before they need any of the above.

This closes the core loop: set up an environment, understand the architecture, build a kernel, contribute changes upstream, and debug problems along the way.
