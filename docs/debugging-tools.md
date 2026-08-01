# Debugging Tools

Kernel bugs are harder to chase than user-space bugs: there is no libc to fall back on, a crash can take down the whole machine, and stack traces are not always symbolized by default. These tools cover most day-to-day needs.

## printk and dynamic debug

`printk()` remains the most common debugging tool. Rather than sprinkling permanent `printk` calls, use dynamic debug to enable verbose logging at runtime for specific files or functions:

```bash
echo 'file drivers/net/ethernet/example.c +p' > /sys/kernel/debug/dynamic_debug/control
```

## ftrace

ftrace traces function calls, scheduling events, and custom tracepoints with very low overhead, and is built into the kernel:

```bash
cd /sys/kernel/tracing
echo function > current_tracer
echo my_driver_probe > set_ftrace_filter
cat trace
```

## kgdb / kdb

For stepping through kernel code with a real debugger, `kgdb` connects a remote GDB session over serial or network to a target kernel built with `CONFIG_KGDB`. `kdb` provides a lighter-weight, built-in shell for inspecting state without a host machine.

## Crash analysis

When a kernel oopses, the printed stack trace can be resolved to file/line information with `scripts/decode_stacktrace.sh`, given a kernel build with debug symbols. For reproducible crashes, KASAN (`CONFIG_KASAN`) and lockdep (`CONFIG_PROVE_LOCKING`) catch entire classes of memory-safety and locking bugs long before they cause a hard-to-diagnose crash.

## A practical workflow

Start with dynamic debug and printk for a rough picture, reach for ftrace when timing or call order matters, and only bring out kgdb when you need to inspect live state that logging cannot capture. Keeping KASAN and lockdep enabled in a development kernel catches many bugs before they need any of the above.

This closes the core loop: set up an environment, understand the architecture, build a kernel, contribute changes upstream, and debug problems along the way.
