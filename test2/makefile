CC      := gcc
B_OUT_DIR := bin
COVERAGE_OUT_DIR := coverage
TEST_OBJECT := hello
SRC_FILE := src/$(TEST_OBJECT).c
INFO_FILE := $(TEST_OBJECT).info
LCOV_OUT_DIR := result

CFLAGS := $(shell if [ ! -e $(B_OUT_DIR) ];then mkdir -p $(B_OUT_DIR); fi) -Wall
TARGET = a b 

.PHONY: all clean $(TARGET)

all: $(TARGET)

a: a.c $(SRC_FILE)
	${CC} ${CFLAGS} -o $(B_OUT_DIR)/$@ $^
	./$(B_OUT_DIR)/$@
	@if [ -e $(COVERAGE_OUT_DIR) ]; then\
        mv *.gcno $(COVERAGE_OUT_DIR);\
        mv *.gcda $(COVERAGE_OUT_DIR);\
		rename 's/$(TEST_OBJECT)/$(TEST_OBJECT)_$@/' $(COVERAGE_OUT_DIR)/$(TEST_OBJECT).*;\
    fi

b: b.c $(SRC_FILE)
	${CC} ${CFLAGS} -o $(B_OUT_DIR)/$@ $^
	./$(B_OUT_DIR)/$@
	@if [ -e $(COVERAGE_OUT_DIR) ]; then\
        mv *.gcno $(COVERAGE_OUT_DIR);\
        mv *.gcda $(COVERAGE_OUT_DIR);\
		rename 's/$(TEST_OBJECT)/$(TEST_OBJECT)_$@/' $(COVERAGE_OUT_DIR)/$(TEST_OBJECT).*;\
    fi

coverage: CFLAGS += $(shell if [ ! -e $(COVERAGE_OUT_DIR) ];then mkdir -p $(COVERAGE_OUT_DIR); fi)
coverage: CFLAGS += -ftest-coverage -fprofile-arcs
coverage: all

coverage_lcov: coverage
coverage_lcov:
	lcov -d ${COVERAGE_OUT_DIR} -o ${COVERAGE_OUT_DIR}/${INFO_FILE} -b . -c
	genhtml -o ${COVERAGE_OUT_DIR}/${LCOV_OUT_DIR} ./${COVERAGE_OUT_DIR}/${INFO_FILE}

clean: 
	rm -rf $(COVERAGE_OUT_DIR)
	rm -rf $(B_OUT_DIR)