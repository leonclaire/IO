The easiest way to read/write port value
and call acpi method.

Code is based on openlibsys.

Attention:

    1. no trojan, no backdoor... 
    2. all free and shareable.
    
Interface:

    BOOL  rp8(WORD, PBYTE);
    BOOL  wp8(WORD, BYTE);
    BOOL  rm8(DWORD_PTR, PBYTE, DWORD);
    BOOL  wm8(DWORD_PTR, PBYTE, DWORD);
    BOOL  OA();
    BOOL  op(PCSTR);
    BOOL  cm(PCSTR);
    BOOL  pn(DWORD);
    BOOL  ps(PCSTR);
    BOOL  pb(PBYTE, DWORD);
    BOOL  gn(PDWORD);
    BOOL  gs(PSTR, DWORD);
    BOOL  gb(PBYTE, DWORD);

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
        DWORD d = 123;
        CHAR s1[200];
        CHAR s2[200];
        CHAR s3[200];
        CHAR s4[200];
        BYTE b[3] = { 7, 8, 9 };

        OA();

        op("_SB_.PCI0.LPCB.BAT1");

        pn(0);

        cm("BIFX");

        for (int i = 0; i < 9; i++)
        {
            gn(&d);
        }

        gs(s1, 200);
        gs(s2, 200);
        gs(s3, 200);
        gs(s4, 200);

        cout << s1 << endl;
        cout << s2 << endl;
        cout << s3 << endl;
        cout << s4 << endl;

        pn(1);

        cm("BIFX");

        for (int i=0; i<16;i++)
        {
            gn(&d);
        }

        gs(s1, 200);
        gs(s2, 200);
        gs(s3, 200);
        gs(s4, 200);

        cout << s1 << endl;
        cout << s2 << endl;
        cout << s3 << endl;
        cout << s4 << endl;
        //BYTE vvv;
        //ReadIO(0x60, &vvv);
        //ReadIO(0x64, &vvv);

        //BYTE buffer[512];
        //rm8(0x000E5E30, buffer, 512);

        //buffer[0x1d] = 0x41;
        //wm8(0x000E5E30, buffer, 512);

        return 0;
    }
