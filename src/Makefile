CPP		        = g++
RM		        = rm -f
CPPFLAGS	    = -Wall -c -I. -O2 -flto -std=c++11 -g
LD		        = g++
LD_FLAGS	    = -Wall -shared -O2
SHARED_LIB	    = libreactcpp-mongo.so
STATIC_LIB	    = $(SHARED_LIB:%.so=%.a)
SOURCES		    = $(wildcard *.cpp */*.cpp)
SHARED_OBJECTS	= $(SOURCES:%.cpp=%.o)
STATIC_OBJECTS	= $(SOURCES:%.cpp=%.s.o)

all:	shared static

shared:	${SHARED_OBJECTS} ${SHARED_LIB}

static:	${STATIC_OBJECTS} ${STATIC_LIB}

${SHARED_LIB}: ${SHARED_OBJECTS}
	${LD} ${LD_FLAGS} -o $@ ${SHARED_OBJECTS} -lreactcpp -lev -lmongoclient -lvariant

${STATIC_LIB}: ${STATIC_OBJECTS}
	ar rcs ${STATIC_LIB} ${STATIC_OBJECTS}

clean:
	${RM} *.obj *~* ${SHARED_OBJECTS} ${STATIC_OBJECTS} ${SHARED_LIB} ${STATIC_LIB}

${SHARED_OBJECTS}:
	${CPP} ${CPPFLAGS} -fpic -o $@ ${@:%.o=%.cpp}

${STATIC_OBJECTS}:
	${CPP} ${CPPFLAGS} -o $@ ${@:%.s.o=%.cpp}

