**C++:**

Lets create `hello_world_2.c` including the following C++ codes:
```c++
#include <iostream>
using namespace std;
int main()
{
    cout << "Hello, World! This is a native C++ program compiled on the command line." << endl;
}
```

Use the following to compile and run the above C++ codes:
```bash
srun -p Interactive --pty /bin/bash
module load openmpi
mpic++/mpiCC/mpicxx --output/-o test2 hello_world_2.c
./test2
```
