# Mindestens diese Parameter MÜSSEN IMMER an gcc übergeben werden!
# Es ist erlaubt, Optionen für striktere Warnungen hinzuzufügen.
CFLAGS := -std=c99 -g -Wall -Wmissing-prototypes -Werror
# Sie dürfen weitere (aber nur von Ihnen geschriebene) C-Dateien oder Header
# verwenden, wenn Sie möchten. Fügen Sie dazu einfach die Dateinamen der
# entsprechenden Liste hinzu, z.B.: SOURCES := dungeon.c mario.c luigi.c yoshi.c
SOURCES := jumpandrun.c
HEADERS := jumpandrun.h

# Alles, was unter dieser Linie steht, darf NICHT verändert werden!
#-------------------------------------------------------------------------------

compile: $(SOURCES) $(HEADERS)
	tests/unerlaubtes.sh
	gcc $(CFLAGS) $(SOURCES) -o jumpandrun

compile_fsanitize: $(SOURCES) $(HEADERS)
	gcc $(CFLAGS) $(SOURCES) -o jumpandrun_fsanitize \
		-fsanitize=address -fsanitize=undefined

clean:
	rm -f jumpandrun jumpandrun_fsanitize Diese_Datei_sollte_nicht_schreibbar_sein.txt
	rm -rf ausgabe diff valgrind

valgrind_korrekte_optionen: compile
	tests/valgrind_korrekte_optionen.sh

valgrind_fehlerhafte_optionen: compile
	tests/valgrind_fehlerhafte_optionen.sh

valgrind: valgrind_korrekte_optionen valgrind_fehlerhafte_optionen

fsanitize: compile_fsanitize
	tests/fsanitize.sh

aufrufe: compile
	tests/aufrufe.sh

stack: compile_fsanitize
	tests/stack.sh

codestyle:
	tests/codestyle.sh

run: valgrind aufrufe fsanitize stack codestyle

