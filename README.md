# route_io
async route tcp/udp data to your c/c++ function, create one instance to handler different protocol and port at one time


## For Linux OS build

## Prerequisition Installed

lock-free-queue-and-stack -- https://github.com/Taymindis/lock-free-stack-and-queue.git


## Installation

```bash
mkdir build

cd build

cmake ..

make

sudo make install

```



## Uninstallation

```bash
cd build

sudo make uninstall

```


## Example to run
```c

void read_data(rio_request_t *req);
void read_data(rio_request_t *req) {
  char *a = "CAUSE ERROR FREE INVALID";

  if (strncmp( (char*)req->in_buff->start, "ERROR", 5) == 0) {
    free(a);
  }
  // printf("%d,  %.*s\n", i++, (int) (req->in_buff->end - req->in_buff->start), req->in_buff->start);
  rio_write_output_buffer_l(req, req->in_buff->start, (req->in_buff->end - req->in_buff->start));
  // printf("%d,  %.*s\n", i++, (int) (req->out_buff->end - req->out_buff->start), req->out_buff->start);
}

int main(void) {

  rio_instance_t * instance = rio_create_routing_instance(24, NULL, NULL);
  rio_add_udp_fd(instance, 12345, read_data, 1024, NULL);
  rio_add_tcp_fd(instance, 3232, read_data, 64, NULL);

  rio_start(instance);

  return 0;
}

```


## for Windows os build

#### Download the Dev-C++ IDE - https://sourceforge.net/projects/orwelldevcpp/

#### go to route_io directory and open routeio_windows.dev, and build it from Dev-C++ IDE.

#### You can use any IDE/build tools as you wish, just add route_io.c route_io.h to your project




