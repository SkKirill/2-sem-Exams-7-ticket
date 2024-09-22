program Project2;

{$APPTYPE CONSOLE}

uses
  SysUtils;

type
  TFileInf = record
    Name: String[100];
    Size: Integer;
    CreationDate: Integer;
  end;

  TList = ^TNode;

  TNode = record
    Data: TFileInf;
    Next: TList;
  end;

  TMyFile = file of TFileInf;

procedure AddToList(var pHead: TList; pEl: TFileInf);
var
  p, q, k: TList;
begin
  if pHead = nil then
    begin
      New(pHead);
      pHead^.Data := pEl;
      pHead^.Next := nil;
    end
  else
    begin
      p := pHead;
      q := p;
      while (p <> nil) and (p^.Data.Name > pEl.Name) do
        begin
          q := p;
          p := p^.Next;
        end;

      New(k);
      k^.Data := pEl;
      if p = pHead then
        begin
          k^.Next := pHead;
          pHead := k;
        end
      else
        begin
          q^.Next := k;
          k^.Next := p;
        end;
    end;
end;

procedure ReadTypeFile(var pList: TList; var pFile: TMyFile);
var
  currentElement: TFileInf;
begin
  while not Eof(pFile) do
    begin
      Read(pFile, currentElement);
      if Pos('.txt', currentElement.Name) <> 0
        then AddToList(pList, currentElement);
    end;
end;

procedure WriteToTextfile(var TextFile: Textfile; pEl: TFileInf);
begin
  Write(TextFile, pEl.Name + ' | ');
  Write(TextFile, (IntToStr(pEl.Size) + ' | '));
  Write(TextFile, (IntToStr(pEl.CreationDate) + ' | '));
  Writeln(TextFile);
end;

procedure PrintListToTexFile(pList: TList; var TxtFile:TextFile);
begin
  while pList <> nil do
    begin
      WriteToTextfile(TxtFile, pList^.Data);
      pList := pList^.Next;
    end;
end;

var
  FType: TMyFile;
  MyList: TList;
  FTxt: TextFile;
begin
  AssignFile(FType, 'TestTypeFile');
  Reset(FType);

  ReadTypeFile(MyList, FType);

  AssignFile(FTxt, 'ReportFile.txt');
  Rewrite(FTxt);

  PrintListToTexFile(MyList, FTxt);

  CloseFile(FType);
  CloseFile(FTxt);
end.

