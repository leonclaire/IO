The easiest way to read/write ec port
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

    VOID ITEReadSpace(WORD, BYTE*);
    VOID ITEWriteSpace(WORD, BYTE);

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

    VOID ITEReadSpace(WORD, BYTE*);
    VOID ITEWriteSpace(WORD, BYTE);

    class ACPI
    {
    public:
        VOID zi();
        ACPI(DWORD, DWORD);
        virtual ~ACPI();

        BOOL op(PCSTR);
        BOOL cm(PCSTR);
        BOOL pn(DWORD);
        BOOL ps(PCSTR);
        BOOL pb(PBYTE, DWORD);
        BOOL pp(PBYTE, DWORD);
        BOOL gn(DWORD*);
        BOOL gs(PSTR, DWORD);
        BOOL gb(PBYTE, DWORD);
        BOOL gp(PBYTE, DWORD);

    private:
        PVOID reserve1;
        PVOID reserve2;
    };

    int main()
    {
        DWORD d = 0xFF;

        CHAR o1[128] = {0};
        CHAR o2[64];
        CHAR o3[64];
        CHAR o4[64];

        OA();

        ACPI acpier(100, 2048);

        acpier.op("_SB_.PCI0.LPCB.BAT1");
        acpier.pn(1);

        CTime s = CTime::GetTickCount();

        ULONG cnt = 0;
        while (++cnt < 10)
        {
            acpier.cm("BIFX");
            cout << cnt << endl << endl;;

            for (int i = 0; i < 16; i++)
            {
                acpier.gn(&d);
                cout << d << endl;
            }

            acpier.gs(o1, 64);
            acpier.gs(o2, 64);
            acpier.gs(o3, 64);
            acpier.gs(o4, 64);

            cout << o1 << endl;
            cout << o2 << endl;
            cout << o3 << endl;
            cout << o4 << endl << endl;

            cout << cnt << endl;
        }

        CTime e = CTime::GetTickCount();

        CTimeSpan diff = e - s;

        cout << diff.GetTotalSeconds() << endl;

        rp8(0x60, &vvv);
        rp8(0x64, &vvv);

        BYTE buffer[512];
        rm8(0x000E5E30, buffer, 512);

        buffer[0x1d] = 0x49;
        wm8(0x000E5E30, buffer, 512);

        for (size_t i = 0; i < 255; i++)
        {
            ITEReadSpace(i, &data);
        }
        
        BYTE b[255] = {0};
        MMIO test(0xBFED9000, 2048);
        int i = 0;
        while (++i < 10)
        {
            test.rm8(0x18, 255, b);
            CString t;
            t.Format("%s", b);
            cout << t << endl;
            Sleep(1000);
        }

        test.rm8(0x18, 255, b);
        return 0;
    }
