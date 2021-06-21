# Copyright (C) 2019-2021 EDF R&D
#
# This library is free software; you can redistribute it and/or
# modify it under the terms of the GNU Lesser General Public
# License as published by the Free Software Foundation; either
# version 2.1 of the License, or (at your option) any later version.
#
# This library is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# Lesser General Public License for more details.
#
# You should have received a copy of the GNU Lesser General Public
# License along with this library; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307 USA
#
# See http://www.salome-platform.org/ or email : webmaster.salome@opencascade.com
#
INCLUDE_DIRECTORIES(
  ${PYTHON_INCLUDE_DIR}
)

ADD_DEFINITIONS(
  ${PYTHON_DEFINITIONS}
)

SET(_link_LIBRARIES
  ${PYTHON_LIBRARIES}
)

SET(_py2cpp_sources
  TypeConversions.cxx
  PyFunction.cxx
  Errors.cxx
  PyPtr.cxx
)

SET(_py2cpp_headers
  py2cppExports.hxx
  TypeConversions.hxx
  PyFunction.hxx
  Errors.hxx
  PyPtr.hxx
  Result.hxx
  py2cpp.hxx
)

ADD_LIBRARY(py2cpp ${_py2cpp_sources})
TARGET_LINK_LIBRARIES(py2cpp ${_link_LIBRARIES})
TARGET_INCLUDE_DIRECTORIES(py2cpp PUBLIC
                          $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
                          $<INSTALL_INTERFACE:include>)

INSTALL(TARGETS py2cpp EXPORT Py2cppCfg LIBRARY DESTINATION lib)
INSTALL(FILES ${_py2cpp_headers} DESTINATION include/py2cpp)
INSTALL(EXPORT Py2cppCfg DESTINATION lib/cmake/py2cpp FILE Py2cppConfig.cmake)

ADD_SUBDIRECTORY(Test)
