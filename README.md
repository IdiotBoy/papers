### 翻译一些英文博客
```c
int main() {
    printf("hello world!");
}



/* However, this is very difficult to achieve in practice since
 * get_online_cpus() not an api which is called all that often.
 *
 */
void cpu_hotplug_begin(void)
{
    cpu_hotplug.active_writer = current;

    cpuhp_lock_acquire();
    for (;;) {
        mutex_lock(&cpu_hotplug.lock);
        if (likely(!cpu_hotplug.refcount))
            break;
        __set_current_state(TASK_UNINTERRUPTIBLE);
        mutex_unlock(&cpu_hotplug.lock);
        schedule();
    }
}
```
