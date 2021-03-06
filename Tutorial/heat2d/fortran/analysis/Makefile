include ../make.settings

override ADIOS2_FINC=`${ADIOS2_DIR}/bin/adios2-config --fortran-flags`
override ADIOS2_FLIB=`${ADIOS2_DIR}/bin/adios2-config --fortran-libs`

default: 
	@echo "Make targets: adios2_stream  adios2_file  hdf5_file"
	@echo "  adios2_stream: build example with ADIOS 2.x step-by-step reading  (heatAnalysis_adios2_stream.F90)"
	@echo "  adios2_file:   build example with ADIOS 2.x for file-only read (heatAnalysis_adios2_file.F90)"
	@echo "  hdf5_file:     build example with HDF5 for file-only read  (heatAnalysis_hdf5_file.F90)"
	@echo "  phdf5_file:    build example with PHDF5 for file-only read  (heatAnalysis_phdf5_file.F90)"


all: default
help: default

print.o : print.F90
	${FC} ${FFLAGS} -c $< 

hdf5_file: print.o heatAnalysis_hdf5_file.F90
	libtool --mode=link --tag=FC ${FC} ${FFLAGS} ${HDF5_FINC} -o heatAnalysis_hdf5_file $^ ${HDF5_FLIB} 

phdf5_file: print.o heatAnalysis_phdf5_file.F90
	libtool --mode=link --tag=FC ${FC} ${FFLAGS} ${PHDF5_FINC} -o heatAnalysis_phdf5_file $^ ${PHDF5_FLIB} 

adios2_file: print.o heatAnalysis_adios2_file.F90
adios2_file: print.o heatAnalysis_adios2_file.F90
	${FC} ${FFLAGS} -o heatAnalysis_adios2_file ${ADIOS2_FINC} $^ ${ADIOS2_FLIB} 

adios2_stream: print.o heatAnalysis_adios2_stream.F90
	${FC} ${FFLAGS} -o heatAnalysis_adios2_stream ${ADIOS2_FINC} $^ ${ADIOS2_FLIB} 


clean-code:
	rm -f *.o *.mod *.fh core.* fort.* 
	rm -f heatAnalysis_adios2_file heatAnalysis_adios2_stream
	rm -f heatAnalysis_hdf5_file heatAnalysis_phdf5_file
	rm -rf .libs

clean-data: 
	rm -rf *.png *.pnm *.bp *.bp.dir

distclean: clean-code clean-data
clean: clean-code clean-data

