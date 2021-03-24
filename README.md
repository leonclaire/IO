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

        CHAR o1[64];
        CHAR o2[64];
        CHAR o3[64];
        CHAR o4[64];

        CHAR o5[5000];
        PIOPACK(o5)->Size = 5000;

        DWORD d1;
        DWORD d2;
        DWORD d3;
        DWORD d4;

        BYTE vvv;

        OA();
        sa(256, 512);

        op("_SB_.PCI0.LPCB.BAT1");
        pn(1);
        cm("BIFX");

        for (int i = 0; i < 16; i++)
        {
            gn(&d);
            cout << d << endl;
        }

        gs(o1, 64);
        gs(o2, 64);
        gs(o3, 64);
        gs(o4, 64);

        cout << o1 << endl;
        cout << o2 << endl;
        cout << o3 << endl;
        cout << o4 << endl << endl;

        ZeroMemory(o1, 64);
        ZeroMemory(o2, 64);
        ZeroMemory(o3, 64);
        ZeroMemory(o4, 64);

        op("_TZ_.TZ00");
        cm("_TMP");
        gn(&d);

        op("_TZ_.TZ01");
        cm("_TMP");
        gn(&d);

        op("");
        ps("Windows 2020");
        cm("_OSI");
        gn(&d);

        cin >> vvv;

        //op("_SB_.PCI0");
        //cm("_PRT");

        //while (1)
        //{
        //    if (!gp(PIOPACK(o5))) break;
        //}

        //BYTE vvv;
        //rp8(0x60, &vvv);
        //rp8(0x64, &vvv);

        //BYTE buffer[512];
        //rm8(0x000E5E30, buffer, 512);

        //buffer[0x1d] = 0x49;
        //wm8(0x000E5E30, buffer, 512);

        return 0;
    }
