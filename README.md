# SendPacket
Nada
library Project1;

{ Important note about DLL memory management: ShareMem must be the
  first unit in your library's USES clause AND your project's (select
  Project-View Source) USES clause if your DLL exports any procedures or
  functions that pass strings as parameters or function results. This
  applies to all strings passed to and from your DLL--even those that
  are nested in records and classes. ShareMem is the interface unit to
  the BORLNDMM.DLL shared memory manager, which must be deployed along
  with your DLL. To avoid using BORLNDMM.DLL, pass string information
  using PChar or ShortString parameters. }

uses
  System.SysUtils,
  windows,
  System.Classes,
  Winapi.Messages,
  System.SysUtils,
  System.Variants,
  System.Classes,
  Vcl.Graphics,
  Vcl.Controls,
  Vcl.Forms,
  Vcl.Dialogs,
  Vcl.ExtCtrls,
  Vcl.StdCtrls,
  Func in 'Func.pas',
  Unit5 in 'Unit5.pas' {MainF},
  Unit1 in 'Unit1.pas';

Var
  ADDR_SENDPACKET  : DWORD = $00405FF0;
  hProcess, hThread, H:Thandle;
Hid: Cardinal;
b: Boolean=false;
 {$R *.res}

  Procedure SendPacket(Buffer : ARRAY OF BYTE; tamanho : DWORD);
 begin
   asm
   push tamanho //Pega o tamanho
   push Buffer //Pega o conteúdo
   call ADDR_SENDPACKET
   end;
   end;




Procedure Chamar;
begin
MainF:= TMainF.Create(Nil);
MainF.ShowModal;
end;

begin
hProcess:=OpenProcess(PROCESS_ALL_ACCESS,B,GetCurrentProcessID);
hThread:=CreateRemoteThread(hProcess, nil,0, @Chamar, @Chamar,0, Hid);
Closehandle(hProcess);
CloseHandle(hThread);

end.

