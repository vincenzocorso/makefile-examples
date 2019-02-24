# Main Settings
BUILD_DIR		:=	build
SRC_DIR			:=	src
INCLUDE_DIR		:=	include
OUTPUT			:=	main

# Makefile setup
CFLAGS			:=	-Wall -std=c11
INCLUDE			:=	-I $(INCLUDE_DIR)
SRCS			:=	$(wildcard $(SRC_DIR)/*.c)
OBJS			:=	$(patsubst $(SRC_DIR)/%.c, $(BUILD_DIR)/%.o, $(SRCS))

$(BUILD_DIR)/$(OUTPUT):		$(OBJS)
				@echo "Linking..."
				@$(CC) $(CFLAGS) $(OBJS) -o $@

$(BUILD_DIR)/%.o:		$(SRC_DIR)/%.c
				@echo "Compiling "$<
				@$(CC) $(CFLAGS) $(INCLUDE) -c $< -o $@

.PHONY:	setup run clean leaks

setup:
	@echo "Starting setup..."
	@mkdir -p $(BUILD_DIR) $(SRC_DIR) $(INCLUDE_DIR) # Create folders if not exists

run:
	@./$(BUILD_DIR)/$(OUTPUT)

clean:
	@echo "Cleaning..."
	@rm -f $(BUILD_DIR)/*.o $(BUILD_DIR)/$(OUTPUT)

leaks:
	@echo "Checking memory leaks..."
	@valgrind --leak-check=yes $(BUILD_DIR)/$(OUTPUT)
