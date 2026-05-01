# Defines phony targets all and clean
.PHONY = all compile clean autoloads tangle

# Emacs invocation
# don't load an init file: -q
# avoid processing X resources: -Q
# send messages to stderr: --batch
EMACS = emacs -Q -q --batch -L ./lisp -L ./site-lisp

# remove command
RM = rm -f

# define compile command (CC)
# call batch-byte-compile function: -f
# CC := -f batch-native-compile
CC := -f batch-byte-compile

# Tangle script
TANGLE_SCRIPT = tangle.el

# default target
all: tangle compile autoloads

# run tangle script (org related)
# the script will tangle the source code blocks from vlm.org
# to compose the init.el final script
tangle:
	${EMACS} ${CC} ${TANGLE_SCRIPT}
	${EMACS} -l ${TANGLE_SCRIPT} -f tangle-and-rename

# compile init.el and early-init.el
compile:
	 ${EMACS} ${CC} init.el early-init.el

autoloads:
	 ${EMACS} -L ./site-lisp -L ./lisp -l ./lisp/lazy-load/lazy-load.el -f lazy-load-update-autoloads

# remove all byte compiled files
clean:
	${RM} *.elc
