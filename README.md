# .travis.yml
language: python
cache: pip
sudo: false
dist: xenial

matrix:
  include:
    - python: "3.6"
      env: TOXENV=lint
    - python: "3.6"
      env: TOXENV=manifest

    - python: "2.7"
      env: TOXENV=py27
    - python: "3.4"
      env: TOXENV=py34
    - python: "3.4"
      env: TOXENV=py34-no-typing
    - python: "3.5"
      env: TOXENV=py35
    - python: "3.6"
      env: TOXENV=py36
    - python: "3.7"
      env: TOXENV=py37
    - python: "pypy"
      env: TOXENV=pypy
      dist: trusty
    - python: "pypy3"
      env: TOXENV=pypy3
      dist: trusty

install:
  - pip install tox

script:
  - tox

before_install:
  - pip install python-coveralls

after_success:
  - tox -e coverage-report
  - coveralls

deploy:
  provider: pypi
  user: theskumar
  password:
    secure: DXUkl4YSC2RCltChik1csvQulnVMQQpD/4i4u+6pEyUfBMYP65zFYSNwLh+jt+URyX+MpN/Er20+TZ/F/fu7xkru6/KBqKLugeXihNbwGhbHUIkjZT/0dNSo03uAz6s5fWgqr8EJk9Ll71GexAsBPx2yqsjc2BMgOjwcNly40Co=
  on:
    tags: true
    repo: theskumar/python-dotenv
