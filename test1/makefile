CC      := gcc
B_OUT_DIR := bin
COVERAGE_OUT_DIR := coverage
INFO_FILE := hello.info
LCOV_OUT_DIR := result

CFLAGS := $(shell if [ ! -e $(B_OUT_DIR) ];then mkdir -p $(B_OUT_DIR); fi) -Wall
TARGET = hello 

.PHONY: all clean $(TARGET)

all: $(TARGET)

hello: hello.c
	${CC} ${CFLAGS} ${LDFLAGS} -o $(B_OUT_DIR)/$@ $^
	./$(B_OUT_DIR)/$@
	mv $@.gcno $(COVERAGE_OUT_DIR)
	gcov -o coverage/ $@.c
	mv $@.c.gcov $(COVERAGE_OUT_DIR)

coverage: CFLAGS += -ftest-coverage -fprofile-arcs -fprofile-dir=$(COVERAGE_OUT_DIR)
coverage: CFLAGS += $(shell if [ ! -e $(COVERAGE_OUT_DIR) ];then mkdir -p $(COVERAGE_OUT_DIR); fi)
coverage: all

coverage_lcov: coverage
coverage_lcov:
	lcov -d ${COVERAGE_OUT_DIR} -o ${COVERAGE_OUT_DIR}/${INFO_FILE} -b . -c
	genhtml -o ${COVERAGE_OUT_DIR}/${LCOV_OUT_DIR} ./${COVERAGE_OUT_DIR}/${INFO_FILE}

clean: 
	rm -rf $(COVERAGE_OUT_DIR)
	rm -rf $(B_OUT_DIR)