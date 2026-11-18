PYTHON=/usr/bin/python3
COBCD=COBCDEVEL=1 $(PYTHON) ../../cobcd

# check that a warning quoting a latin-9 byte does not make cobcd fail

.PHONY : test testprod clean

test:
	LC_ALL=C $(COBCD) -x -Wall test.cbl > under-test.txt 2>&1
# expected warning (exact wording may vary with the cobc version):
#   test.cbl:7: warning: numeric value is expected [-Wtyping]
	grep -aq "warning:" under-test.txt
# this cobcd message must not appear (it is shown when the decoding fails):
#   #### Exception only because of additional options, possibly bad cobc version?
	! grep -aq "Exception only" under-test.txt
	test -x test

testprod:
	$(MAKE) test COBCD=cobcd

clean:
	rm -f test under-test.txt
