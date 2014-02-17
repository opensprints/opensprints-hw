VERSION  := $(shell cat VERSION)
OUTDIR   = out
FILEBASE = roller_sensor_$(VERSION)_gerber

all: output_zip

version:
	@echo $(VERSION)

gerber:
	mkdir -p $(OUTDIR)
	@echo "Open PCBnew and plot the gerber files and generate the " \
		"drill report, saving the files in the ${OUTDIR} directory."
	@read -p "Press ENTER when done." foo

output_tar: gerber
	cd $(OUTDIR) ; \
	tar -jcvf ${FILEBASE}.tar.bz2 *.pho *.drl *-drl.rpt ; \
	cd -

output_zip: gerber
	cd $(OUTDIR) ; \
	zip -r ${FILEBASE}.zip *.pho *.drl *-drl.rpt ; \
	cd -

output_barebones: gerber
	cd $(OUTDIR) ; \
	zip -r ${FILEBASE}_barebones.zip \
			${FILEBASE}-Component.pho \
			${FILEBASE}-Copper.pho \
			${FILEBASE}-Edges_Pcb.pho \
			${FILEBASE}.drl ; \
	cd -

clean:
	rm -f $(OUTDIR)
