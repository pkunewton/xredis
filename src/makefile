TARGET= ./redis-server

CFLAGS := -Wall -w   -g -O0  -Wno-unused -Wno-sign-compare -Wno-deprecated-declarations -Wno-deprecated -Wl,--no-as-needed -std=c++11 #-DUSE_JEMALLOC
cppfiles := $(shell ls *.cpp)
cfiles := $(-shell ls *.c)
OBJS := $(patsubst %.cpp,./%.o, $(cppfiles) $(cfiles))
COBJS=${patsubst %.c,./%.o,$(cfiles)}
CXXOBJS=${patsubst %.cpp,./%.o,$(cppfiles)}

DEPS=$(patsubst %.o,%.d,$(OBJS))

LIB= #../libjemalloc.a  #/usr/lib64/libprofiler.so



SO_LIB= 

.PHONY: all clean

all: ${TARGET}

${TARGET}: ${OBJS} ${LIB} 
	${CXX} -lrt -o $@ $^ ${LDFLAGS}${LIB} ${LIB64} -lpthread

${CXXOBJS}:./%.o:./%.cpp
	${CXX} -MMD -c -o $@ $< ${CFLAGS} 

${COBJS}:./%.o:.%.c
	${CC} -MMD -c -o $@ $< ${CFLAGS} 

-include $(DEPS)

clean:
	rm -f ${OBJS} ${TARGET} ${DEPS}

show:
	@echo GPROF=$(GPROF)
	@echo CFLAGS=$(CFLAGS)
	@echo LDFLAGS=$(LDFLAGS)
	@echo objs=$(OBJS)
	@echo cppfiels=$(cppfiles)
	@echo cfiels=$(cfiles)
	@echo DEPS=$(DEPS)
	@echo CXXOBJS=$(CXXOBJS)
	@echo COBJS=$(COBJS)

