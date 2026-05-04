# Makefile for libmodbus program
# Example: Print important variables when make starts
$(info === Build Information ===)

#assigne gcc compiler to CC variable
CC      = gcc
#assigne c flags to CFLAGS variable
CFLAGS	= -Wall -Wextra -O3 -g -DON=1 -MMD
LDFLAGS	= 

#assigne linker flag to MODBUS_LIBS ,pkg-config will take care of linker flag (-l and -L)
MODBUS_LIBS	:= $(shell pkg-config --libs libmodbus)

# assigne include path of modbus to CFLAGS variable
CFLAGS  += -I/usr/local/include/modbus
LDFLAGS += $(MODBUS_LIBS)

#creating targert for program
BUILD_DIR	= build
TARGET  = $(BUILD_DIR)/bin
#assigne sorce file to SRC variable
SRC	= hello.c source1.c
#creating object file of all source file and copy it to into build directory and  assigne it to OBJ
OBJ	=$(addprefix $(BUILD_DIR)/,$(SRC:.c=.o))
#creating dependency file of all object file	
DEP	=$(OBJ:.o=.d)

#all is the first target in the make file when we type make it look for all.it will first look for target variable.
all:$(TARGET)

#TARGET variable look for object variable
$(TARGET): $(OBJ)
	$(CC) $(OBJ) -o $(TARGET) $(LDFLAGS)
#it will create the object file for all source file
$(BUILD_DIR)/%.o: %.c
	@mkdir -p $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

#this line tell the make to read the .d file which contain the rule (.o and .h),it tell make if you modify .h file it should# regenerate the .o file
-include $(DEP)
clean:
	rm -rf $(TARGET) $(BUILD_DIR)
	rm -f $(TARGET)
	rm -rf $(OBJ)
	rm -rf $(DEP)

.PHONY: all clean
	

