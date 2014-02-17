VERSION  := $(shell cat VERSION)
OUTDIR   = out
FILEBASE = roller_sensor_$(VERSION)_gerber
GERBER_EXTS = *.drl *.gbl *.gbo *.gbr *.gbs *.gtl *.gto *.gts *.pho *.rpt

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
	tar -jcvf ${FILEBASE}.tar.bz2 $(GERBER_EXTS) ; \
	cd -

output_zip: gerber
	cd $(OUTDIR) ; \
	zip -r ${FILEBASE}.zip $(GERBER_EXTS) ; \
	cd -

output_barebones: gerber
	cd $(OUTDIR) ; \
	zip -r ${FILEBASE}_barebones.zip \
			${FILEBASE}-Component.pho \
			${FILEBASE}-Component.gtl \
			${FILEBASE}-Copper.pho \
			${FILEBASE}-Copper.gbl \
			${FILEBASE}-Edges_Pcb.pho \
			${FILEBASE}-PCB_Edges.gbr \
			${FILEBASE}.drl ; \
	cd -

clean_archives:
	rm -f \
		$(OUTDIR)/$(FILEBASE)_barebones.zip \
		$(OUTDIR)/$(FILEBASE).zip \
		$(OUTDIR)/$(FILEBASE).tar.bz2

clean:
	rm -rf $(OUTDIR)
