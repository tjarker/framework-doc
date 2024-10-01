
project-plan.pdf: project-plan.tex gantt.pdf
	@latexmk -pdf project-plan.tex

gantt.pdf: gantt.mmd conf.json Makefile
	docker run --rm -u `id -u`:`id -g` -v ${shell pwd}:/data minlag/mermaid-cli -i $< -o $@ -t neutral -e pdf -f -c conf.json \
		-w 2500 -H 400