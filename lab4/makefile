# Detecting OS
UNAME_S=$(shell uname -s)
ifeq ($(UNAME_S),Linux)
    CC=g++-4.8
else
    ifeq ($(UNAME_S),Darwin)
        CC=g++-4.8
    else
        CC=g++
    endif
endif

# compiler flags for debug
CPPFLAGS=-std=c++11 -Wall -g -DDEBUG

# name of the binary
all: lab4

# First we map every source code to its object file.
# We do this separately for each source file to better identify the header dependency.

main.o: main.cpp BoundedList.h BoundedListImpl.h
	$(CC) -c $< -o $@ $(CPPFLAGS)

Data.o: Data.cpp Data.h
	$(CC) -c $< -o $@ $(CPPFLAGS)

# Now it's time to link both objects. No need for -I argument anymore.
lab4: Data.o main.o
	${CC} $^ -o $@ ${CPPFLAGS}

# Memory check rule. Depends on a fresh binary.
.PHONY: memcheck
memcheck: lab4
	valgrind --tool=memcheck ./$<

# The clean rule
.PHONY: clean
clean:
	-@rm *.o lab4 *~ 2>/dev/null || true
