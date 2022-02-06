
## Usage

cd ..

make rebound-up

make rebound-python-example

make rebound-python-example  CONTAINER_ENGINE=docker OS_IMAGE_VERSION=20.04

make rebound-python-example  CONTAINER_ENGINE=docker OS_IMAGE_VERSION=19.04

make rebound-python-example PYTHON_EXAMPLE=simple_orbit/problem.py

make rebound-python-example PYTHON_EXAMPLE=outersolarsystem
make rebound-python-example PYTHON_EXAMPLE=horizons
make rebound-python-example PYTHON_EXAMPLE=orbital_elements
make rebound-python-example PYTHON_EXAMPLE=longtermtest
make rebound-python-example PYTHON_EXAMPLE=simulationarchive
make rebound-python-example PYTHON_EXAMPLE=megno_simple
make rebound-python-example PYTHON_EXAMPLE=simple_orbit
make rebound-python-example PYTHON_EXAMPLE=megno
make rebound-python-example PYTHON_EXAMPLE=dragforce

`make print-PYTHON_EXAMPLES`


`PYTHON_EXAMPLES = ./outersolarsystem/problem.py ./horizons/problem.py ./orbital_elements/problem.py ./longtermtest/problem.py ./megno_interactive/problem.py ./simulationarchive/problem.py ./megno_simple/problem.py ./.gitignore ./simple_orbit/problem.py ./megno/problem.py ./dragforce/problem.py`