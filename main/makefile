compile: main.cpp
	g++ -g  main.cpp -I ../trunk/src/  ../trunk/src/client/linux/libbreakpad_client.a  ../trunk/src/libbreakpad.a  -lpthread -o main
run: main
	rm -f /tmp/*.dmp
	./main &
stack:
	../trunk/src/tools/linux/dump_syms/dump_syms ./main > main.sym
	rm -rf ./symbols/main/`head -n1 main.sym | awk '{ print $$4}'`
	mkdir ./symbols/main/`head -n1 main.sym | awk '{ print $$4}'`
	mv main.sym ./symbols/main/`head -n1 main.sym | awk '{ print $$4}'`
	cp /tmp/*.dmp minidump.dmp
	../trunk/src/processor/minidump_stackwalk minidump.dmp ./symbols


all: compile run stack
