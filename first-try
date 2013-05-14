#include < stdio.h >

// kernel (liniar) -> ruleaza pe un singur thread; output / input;
// CPU -> lanseaza programul pe mai multe thread-uri in paralel;
// __global__ -> recunoscut de CUDA; specificator ( urmataorea secventa de cod -> kernel);
// d_in / d_out -> alocate pe GPU;
/*

Fiecare thread isi cunoaste indexul
In CUDA avem o variabila numita threadIdx -> index-ul pentru fiecare thread;
Lansam 64 de thead-uri; pentru fiecare instanta a acestor thread-uri;

*/


/* kernel<<<grid of blocks(1,2,3D), block of threads(1,2,3D)>>>(output,input);
   kernel<<<dim3(bx,by,bz), dim3(tx,ty,tz),shmem(shared memory per block in bytes>>>(output,input);
   - grid of blocks = bx*by*bz
   - block of threads = tx*ty*tz
   threadIdx: thread within block; threadIdx.x , threadIdx.y
   blockDim: size of a block
   blockId: block within grid
   gridDim: size of grid
- 1D -> dim3(x,y,z) = dim3(x,1,1) = dim3(x) = x;
- putem rula mai multe block-uri in acelasi timp;
- nnumar maxim de thread-uri per block -> 512 (old gpu) / 1024 (new gpu)
*/

__global__ void square(float * d_out, float * d_in) {

    int idx = threadIdx.x;
    float f = d_in[idx];
    d_out[idx] = f * f;

}


int main(int argc, char * * argv) {

    const int ARRAY_SIZE = 64;
    const int ARRAY_BYTES = ARRAY_SIZE * sizeof(float);

    // generam un vector ( input) asupra host-ului
    float h_in[ARRAY_SIZE];
    for (int i = 0; i < ARRAY_SIZE; i++) {

        h_in[i] = float(i);

    }

    float h_out[ARRAY_SIZE];

    //GPU Memory pointers

    float * d_in;
    float * d_out;

    // allocate GPU memory

    cudaMalloc((void * * )) & d_in, ARRAY_BYTES);
cudaMalloc((void * * )) & d_out, ARRAY_BYTES);

// transfer catre GPU

cudaMemcpy(d_in, h_in, ARRAY_BYTES, cudaMemcpyHostToDevice);

//lansam kernel

square << < 1, ARRAY_SIZE >>> (d_out, d_in);
// 64 de copi a kernel-ului pe 64 de thread-uri;


// transfer de la GPU catre CPU

cudaMemcpy(h_out, d_out, ARRAY_BYTES, cudaMemcpyDeviceToHost);

for (int i = 0; i < ARRAY_SIZE; i++) {

    printf("%f", h_out[i]);
    printf(((i % 4) != 3) ? "\t" : "\n");

}

cudaFree(d_int);
cudaFree(d_out);

return 0;
}
