# SET THE COSMOS SOFTWARE HOME FOLDER
COSMOSHOME = ..
SUPPORT = $(COSMOSHOME)/support
DEVICE = $(COSMOSHOME)/device
TESTBED = $(COSMOSHOME)/testbed
THIRDPARTY = $(COSMOSHOME)/thirdparty

OBJECTS = $(patsubst %.cpp,%.o,$(wildcard *.cpp))
EXECUTABLES = $(patsubst %.cpp,%,$(wildcard *.cpp))
SUPPORT_LIB = $(SUPPORT)/libCosmosSupport.a
SUPPORT_INC = $(wildcard $(SUPPORT)/*.h)
SUPPORT_CPP = $(wildcard $(SUPPORT)/*.cpp)
DEVICE_LIB = $(DEVICE)/libCosmosDevice.a
DEVICE_INC = $(wildcard $(DEVICE)/*.h)
DEVICE_CPP = $(wildcard $(DEVICE)/*.cpp)

CFLAGS = -pg -g -pedantic -Wall -I$(SUPPORT) -I$(DEVICE) -I$(THIRDPARTY)

LFLAGS = -L$(SUPPORT) -L$(DEVICE) -lm -lCosmosSupport -lCosmosDevice -lpthread

%.o : %.c
	gcc -c $(CFLAGS) $<

%.o : %.cpp $(SUPPORT_INC) $(DEVICE_INC)
	g++ -c $(CFLAGS) $<

% : %.cpp $(SUPPORT_LIB) $(DEVICE_LIB)
	g++ -c $(CFLAGS) $<
	g++  $(CFLAGS) -o $@ $@.o $(LFLAGS)

% : %.o $(SUPPORT_LIB) $(DEVICE_LIB)
	g++  $(CFLAGS) -o $@ $@.o $(LFLAGS)

all : $(EXECUTABLES)

$(SUPPORT_LIB) : $(SUPPORT_CPP) $(SUPPORT_INC)
	$(MAKE) -C $(SUPPORT)

$(DEVICE_LIB) : $(DEVICE_CPP) $(DEVICE_INC)
	$(MAKE) -C $(DEVICE)

# CLEAN ALL THE PRODUCED FILES
clean: 
	rm -f *.o *.a makefileq* obj release debug *.user $(EXECUTABLES)
