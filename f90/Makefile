FC=pgf90
ifeq ($(TARGET),gpu)
	FCFLAGS=-O3 -Mpreprocess -ta=nvidia -fast -Minfo=all,intensity,ccff
	LDFLAGS=-ta=nvidia
else
	FCFLAGS=-O3 -Mpreprocess -mp
	LDFLAGS=-mp
endif

cg.x: matrix.o vector.o main.o
	${FC} -o $@ ${LDFLAGS} $^

matrix.o: matrix.F90
vector.o: vector.F90
main.o: main.F90

.SUFFIXES: .o .F90
.F90.o:
	${FC} ${FCFLAGS} $< -c -o $@

.PHONY: clean
clean:
	rm -Rf cg.x pgprof* *.o *.mod core
