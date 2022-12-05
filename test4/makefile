CC      := gcc
B_OUT_DIR := bin
COVERAGE_OUT_DIR := coverage
TEST_OBJECT := hello
SRC_FILE := src/$(TEST_OBJECT).c
COVERAGE_OUT_DIR := coverage
CFLAGS := $(shell if [ ! -e $(B_OUT_DIR) ];then mkdir -p $(B_OUT_DIR); fi) -Wall
TARGET = a b 

.PHONY: all clean $(TARGET)

all: $(TARGET)

a: a.c $(SRC_FILE)
	${CC} ${CFLAGS} -o $(B_OUT_DIR)/$@ $^
	./$(B_OUT_DIR)/$@

b: b.c $(SRC_FILE)
	${CC} ${CFLAGS} -o $(B_OUT_DIR)/$@ $^
	./$(B_OUT_DIR)/$@

coverage: CFLAGS += -ftest-coverage -fprofile-arcs
coverage: all

coverage_gcovr: CFLAGS += $(shell if [ ! -e $(COVERAGE_OUT_DIR) ];then mkdir -p $(COVERAGE_OUT_DIR); fi)
coverage_gcovr: coverage
coverage_gcovr:
	gcovr -r . --html-details $(COVERAGE_OUT_DIR)/${TEST_OBJECT}.html --xml $(COVERAGE_OUT_DIR)/${TEST_OBJECT}.xml

clean: 
	rm -f *.gcno *.gcda
	rm -rf $(COVERAGE_OUT_DIR)
	rm -rf $(B_OUT_DIR)