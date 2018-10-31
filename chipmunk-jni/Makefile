# Chipmunk for Java
# Java bindings for the Chipmunk 2D physics library
# 
# http://github.com/johang/chipmunk-for-java
# 
# Copyright 2010, Johan Gunnarsson, johan.gunnarsson@gmail.com
# 
# Chipmunk for Java is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
# 
# Chipmunk for Java is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# You should have received a copy of the GNU General Public License
# along with Chipmunk for Java.  If not, see <http://www.gnu.org/licenses/>.

JAVA_HOME := /usr/lib/jvm/default-java

ifeq ($(shell uname -s),Darwin)
	platform_ldflags = -L"$(JAVA_HOME)/jre/lib/server"
	target_binary = libchipmunk-jni.dylib
else
	platform_ldflags = -L"$(JAVA_HOME)/jre/lib/amd64/server"
	target_binary = libchipmunk-jni.so
endif

CPPFLAGS = \
	-I"$(JAVA_HOME)/include" \
	-I"$(JAVA_HOME)/include/$(shell uname -s)" \
	-I"../chipmunk/include/chipmunk" \
	-I"./src" \
	-I"../chipmunk-java/include" \
	-MMD \
	-MP \
	-MF"$(@:%.o=%.d)" \
	-MT"$(@:%.o=%.d)" \

CFLAGS := \
	-Wall \
	-fPIC

LDFLAGS := \
	-shared \
	-L".." \
	$(platform_ldflags) \
	-lchipmunk \
	-ljvm \

CHIPMUNKJNI_SRC_FILES := $(wildcard src/*.c)

.PHONY: all clean

all: $(target_binary)

-include $(CHIPMUNKJNI_SRC_FILES:%.c=%.d)

$(target_binary): $(CHIPMUNKJNI_SRC_FILES:%.c=%.o)
	$(CC) -o "$@" $^ $(LDFLAGS)

clean:
	rm -f src/*.o
	rm -f src/*.d
	rm -f $(target_binary)
