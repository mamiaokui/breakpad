compile: main.cpp
	g++ -g  main.cpp -I ../breakpad_project/src/  ../breakpad_project/src/client/linux/libbreakpad_client.a  ../breakpad_project/src/libbreakpad.a  -lpthread -o main
run: main
	rm -f /tmp/*.dmp
	./main &
stack:
	../breakpad_project/src/tools/linux/dump_syms/dump_syms ./main > main.sym
	rm -rf ./symbols/main/`head -n1 main.sym | awk '{ print $$4}'`
	mkdir ./symbols/main/`head -n1 main.sym | awk '{ print $$4}'`
	mv main.sym ./symbols/main/`head -n1 main.sym | awk '{ print $$4}'`
	cp /tmp/*.dmp minidump.dmp
	../breakpad_project/src/processor/minidump_stackwalk minidump.dmp ./symbols


all: compile run stack
