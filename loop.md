### Creating the loop uv_loop_t
###### One can run multiple event loops as long as each runs in a different thread.
#
```c
#include <stdio.h>
#include <stdlib.h>
#include <uv.h>

int main() {
    // Creating a non default loop
    uv_loop_t *loop = malloc(sizeof(uv_loop_t)); // Allocate
    // Syntax: int uv_loop_init(uv_loop_t* loop)
    uv_loop_init(loop); // Initializes the given uv_loop_t structure.

    // Using the default loop
    // Syntax: uv_loop_t* uv_default_loop(void)
    uv_loop_t *main_loop = uv_default_loop();
    
    printf("Now quitting.\n");
    uv_run(loop, UV_RUN_DEFAULT);
    uv_run(main_loop, UV_RUN_DEFAULT);

    uv_loop_close(loop);
    uv_loop_close(main_loop);

    free(loop);
    // free(main_loop);
    return 0;
}

/*
 * NOTE:
 *  This function is DEPRECATED (to be removed after 0.12), users should
 *  allocate the loop manually and use uv_loop_init instead.
 *
 * UV_EXTERN uv_loop_t* uv_loop_new(void);
*/
```

