PYTHON=/usr/bin/python3
COBCD=COBCDEVEL=1 $(PYTHON) ../../cobcd

# check that -MD, -MT and -MF are passed to cobc, which then writes test.d

# cobc 3.3 needs -MD with -MT/-MF, cobc 3.2 has no -MD
MD:=$(shell cobc --help | grep -q -e -MD && echo -MD)

.PHONY : test testprod clean

test:
	rm -f test.d
	LC_ALL=C $(COBCD) -x $(MD) -MT test -MF test.d test.cbl
	test -f test.d

testprod:
	$(MAKE) test COBCD=cobcd

clean:
	rm -f test test.d
