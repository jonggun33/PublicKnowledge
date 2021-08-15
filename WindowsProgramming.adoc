= Programming on Windows
:toc: left
:sectnums:

== Windows API
.Skeleton
====
[source, c++]
#include <Windows.h>
int WINAPI WinMain(HINSTANCE hhInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow) {
	MessageBox(NULL, "Hello World", "Note", MB_OK);
	return 0;
}
====

=== Nomenclature
WINAPI:: __stdcall
HINSTANCE::
LPSTR:: CHAR *LPSTR
MB_OK:: ok


== MFC


== Basic
http://www.functionx.com/visualc/gdi/gdicoord.htm[GDI Coordinate Systems]

https://www.codeproject.com/Questions/605822/ZoomingplususingplusViewport[Zooming using Viewport]

http://www.winprog.org/tutorial/menus.html[Menus and Icons]
