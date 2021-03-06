# ==================================================================================================
# Copyright 2011 Twitter, Inc.
# --------------------------------------------------------------------------------------------------
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this work except in compliance with the License.
# You may obtain a copy of the License in the LICENSE file, or at:
#
#  http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
# ==================================================================================================

PANTS_SOURCES   = rglobs('*.py') - rglobs('bin/*.py')
PANTS_GARBAGE   = rglobs('*.pyc') + rglobs('*~')
PANTS_RESOURCES = rglobs('*') - PANTS_SOURCES - PANTS_GARBAGE

# Only build pylint on py 2.x
def pylint_build_filter():
  import sys
  return sys.version_info[0] == 2

python_library(
  name = 'pants-deps',
  dependencies = [
    python_requirement('elementtree'),
    python_requirement('mako'),  # TODO: Remove after getting rid of the doc command.
    python_requirement('markdown'),
    python_requirement('pygments'),
    python_requirement('pylint', version_filter=pylint_build_filter),
    python_requirement('pystache'),
    python_requirement('pytest'),
    python_requirement('python_daemon'),
  ]
)

python_library(
  name = 'pants-lib',
  dependencies = [
    'src/python/twitter/common',
    'src/python/twitter/common/app',
    'src/python/twitter/common/confluence',
    'src/python/twitter/common/dirutil',
    'src/python/twitter/common/java',
    'src/python/twitter/common/lang',
    'src/python/twitter/common/process',
    'src/python/twitter/common/python',
    ':pants-deps',
  ],
  sources = PANTS_SOURCES,
  resources = PANTS_RESOURCES
)

python_binary(
  name = 'pants',
  dependencies = [
    ':pants-lib',
  ],
  source = 'bin/pants_exe.py',
)

python_binary(
  name = 'ng',
  dependencies = [
    'src/python/twitter/common/app',
    'src/python/twitter/common/log',
  ],
  source = 'java/nailgun_client.py',
)

# TODO(John Sirois): add a BUILD.commons github wiki goal to the 'publish' phase and publish these

page(name = 'readme',
  source = 'README.md',
  dependencies = [
    'src/python/twitter/pants/docs:migration',
    ':install',
  ]
)

page(name = 'install',
  source = 'INSTALL.md',
)
