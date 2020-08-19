The easiest way to read/write port value.

Code is based on openlibsys.

Attention:

    1. no virus, no trojan, no backdoor... 
    2. no copyright, all free and shareable.

How to use:

    1. #pragma comment(lib,"F:\Public\\io.lib")
    2. BOOL ReadPort(WORD port, PBYTE value);
        BOOL WritePort(WORD port, BYTE value);
    3. call api
    4. admin run. 

Sample:

    #pragma comment(lib,"F:\\Public\\io.lib")

    BOOL	ReadPort(WORD port, PBYTE value);
    BOOL	WritePort(WORD port, BYTE value);

    int main()
    {
        BYTE v1, v2;

        ReadPort(0x60, &v1);
        ReadPort(0x64, &v2);

        WritePort(0x60, 0x1);
        WritePort(0x64, 0x1);

        return 0;
    }