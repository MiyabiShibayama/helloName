PYTHON3		= python3
VENV		= .venv
ACTIVATE	= . ./${VENV}/bin/activate
TARGET		= testpypi

.PHONY: usage
usage:
	@echo "Usage: ${MAKE} TARGET"
	@echo ""
	@echo "Targets:"
	@echo "  build-env      build venv directory"
	@echo "  doc            build document"
	@echo "  test           run test scripts"
	@echo "  test_all       run all test VerySlow!!"
	@echo "  clean          remove venv directory"
	@echo ""
	@echo "  build          build package"
	@echo "  upload         upload to ${TARGET}"
	@echo "    TARGET=pypi  upload to pypi"


.PHONY: build-env
build-env:
	@${MAKE} -s ${VENV}
	@${MAKE} -s secrets

${VENV}: requirements.txt
	${PYTHON3} -m venv ${VENV}
	${ACTIVATE} && pip install --upgrade pip setuptools wheel
	${ACTIVATE} && pip install --upgrade -r requirements.txt
	touch ${VENV}

.PHONY: clean
clean:
	rm -rf dist build *egg-info

.PHONY: build
build: ${VENV}
	rm -rf dist build *.egg-info
	${ACTIVATE} && python setup.py sdist bdist_wheel
	${ACTIVATE} && twine check dist/*

.PHONY: upload
upload:
	${MAKE} build
	${ACTIVATE} && twine upload --repository ${TARGET} dist/*
