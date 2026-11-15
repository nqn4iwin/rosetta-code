CC = gcc-13
CFLAGS = -std=c17 -Wall -Wextra -Wpedantic -g

.PHONY: all clean
all: build/hello

build/hello: exercises/hello/main.c
	mkdir -p build
	$(CC) $(CFLAGS) $< -o $@

clean:
	rm -f build/hello
