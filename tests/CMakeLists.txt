# Copyright (c) 2015, Matthijs Möhlmann
# All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are met:
#
#   Redistributions of source code must retain the above copyright notice, this
#   list of conditions and the following disclaimer.
#
#   Redistributions in binary form must reproduce the above copyright notice,
#   this list of conditions and the following disclaimer in the documentation
#   and/or other materials provided with the distribution.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
# AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
# ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE
# LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
# CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
# SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
# INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
# CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
# ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
# POSSIBILITY OF SUCH DAMAGE.

macro (build_and_run arg)
    # Add headers to sources to enable file browsing in IDEs
    add_executable(Sqlpp11PostgreSQL${arg} ${arg}.cpp ${sqlpp_headers})
    target_link_libraries(Sqlpp11PostgreSQL${arg} sqlpp-postgresql ${PostgreSQL_LIBRARIES})
    include_directories("../include")
    target_compile_features(Sqlpp11PostgreSQL${arg} PRIVATE cxx_auto_type)
	target_include_directories(Sqlpp11PostgreSQL${arg} PRIVATE ${PostgreSQL_INCLUDE_DIRS} )
    add_test(${arg} Sqlpp11PostgreSQL${arg})
endmacro ()

macro (build_and_run_dynamic arg)
    add_executable(Sqlpp11PostgreSQL${arg}-dynamic ${arg}.cpp ${sqlpp_headers})
    target_link_libraries(Sqlpp11PostgreSQL${arg}-dynamic sqlpp-postgresql-dynamic dl)
    include_directories("../include")
    target_compile_features(Sqlpp11PostgreSQL${arg}-dynamic PRIVATE cxx_auto_type)
	target_include_directories(Sqlpp11PostgreSQL${arg}-dynamic PRIVATE ${PostgreSQL_INCLUDE_DIRS} )
    add_test(${arg}-dyanmic Sqlpp11PostgreSQL${arg}-dynamic)
endmacro()

build_and_run(BasicTest)
#build_and_run_dynamic(BasicTest)
build_and_run(DateTest)
build_and_run(TypeTest)
build_and_run(TransactionTest)
build_and_run(ConstructorTest)
