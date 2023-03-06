#include<bits/stdc++.h>

using namespace std;

int main()
{
    FILE* fp = fopen("D:\\BasketballPass_416x240_50 (1).yuv", "rb");
    if (!fp) {
        printf("Failed to open input file\n");
        return 1;
    }

    const int width = 416;
    const int height = 240;
    const int frame_size = width * height * 3 / 2;
    unsigned char* frame_data = (unsigned char*)malloc(frame_size);

    int frame_count = 0;
    while (fread(frame_data, 1, frame_size, fp) == frame_size) {
        char output_filename[256];
        sprintf(output_filename, "yuv\\output_%04d.yuv", frame_count);

        FILE* fp_out = fopen(output_filename, "wb");
        if (!fp_out) {
            printf("Failed to create output file %s\n", output_filename);
            break;
        }

        fwrite(frame_data, 1, frame_size, fp_out);
        fclose(fp_out);

        ++frame_count;
        printf("Frame %d saved.\n",frame_count);
    }

    free(frame_data);
    fclose(fp);

    printf("Extracted %d frames\n", frame_count);

    return 0;
}
