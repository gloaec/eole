SRC        := $(wildcard *.tex)
OBJPDF     := $(SRC:tex=pdf)
RM         := rm --force 
TEXPDFPRG  := xelatex
TEXPDFOPT  := -file-line-error
DATE       := `date +'%d%m%Y-%H%M%S'`
BUILDLOG   := build-messages-$(DATE).txt
LATEXBUILD := $(TEXPDFPRG) $(TEXPDFOPT)

define latexbuild
	@echo "Rerun to get cross-references" > $1.log
	@while [ `grep -c "Rerun to get cross-references" $1.log` -ne 0 ] ; \
	do \
		echo $(TEXPDFPRG) $(TEXPDFOPT) $2 ; \
		if ! $(TEXPDFPRG) $(TEXPDFOPT) $2 > ./$(BUILDLOG) ; then \
			cat $*.log ; \
			rm $@ > /dev/null 2>&1 ; \
			echo "ret: $?" ; \
			exit 255 ; \
		fi ; \
	done
endef

all: $(OBJPDF) 

%.pdf: %.tex
	$(call latexbuild, $*, $< ) 
	$(call latexbuild, $*, $< ) 

clean:
	$(RM) *.aux  
	$(RM) *.d 
	$(RM) *.log
	$(RM) *.nav
	$(RM) *.out
	$(RM) *.snm
	$(RM) *.toc
	$(RM) *.txt

fclean: clean
	$(RM) $(OBJPDF)
	$(RM) *.txt

re: fclean all
