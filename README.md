The easiest way to read/write port value.

Code is based on openlibsys.

Attention:

    1. no virus, no trojan, no backdoor... 
    2. no copyright, all free and shareable.

How to use:

    1. #pragma comment(lib,"F:\Public\\io.lib")
    2. BOOL rp8(WORD port, PBYTE value);
       BOOL wp8(WORD port, BYTE value);
    3. call api
    4. admin run. 

Sample code:

    #pragma comment(lib,"F:\\Public\\io.lib")

    BOOL rp8(WORD port, PBYTE value); //ReadPort
    BOOL wp8(WORD port, BYTE value);  //WritePort

    int main()
    {
        BYTE v1, v2;

        rp8(0x60, &v1);
        rp8(0x64, &v2);

        wp8(0x60, 0x1);
        wp8(0x64, 0x1);

        return 0;
    }
