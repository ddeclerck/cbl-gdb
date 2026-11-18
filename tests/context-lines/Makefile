PYTHON=/usr/bin/python3
COBCD=COBCDEVEL=1 $(PYTHON) ../../cobcd

# check that the context lines of a warning are not merged with it

.PHONY : test testprod clean

test:
	LC_ALL=C $(COBCD) -x -Wall test.cbl 2> under-test.txt > /dev/null
# expected warning, alone on its line (exact wording may vary with the cobc version):
#   test.cbl:8: warning: numeric value is expected [-Wtyping]
	grep -aq "warning:" under-test.txt
# must not appear: warning and context on the same line, like
#   test.cbl:8: warning: numeric value is expected [-Wtyping] 6 |        01 W-B PIC 9. ...
	! grep -a "warning:" under-test.txt | grep -aq " [0-9]* [|>] "

testprod:
	$(MAKE) test COBCD=cobcd

clean:
	rm -f test under-test.txt
