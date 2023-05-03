# Programming on Windows
:toc: left
:sectnums:

## Windows API
.Skeleton
====
[source, c++]
#include <Windows.h>
int WINAPI WinMain(HINSTANCE hhInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow) {
	MessageBox(NULL, "Hello World", "Note", MB_OK);
	return 0;
}
====

### Nomenclature
WINAPI:: __stdcall
HINSTANCE::
LPSTR:: CHAR *LPSTR
MB_OK:: ok


## MFC


## Basic
[GDI Coordinate Systems](http://www.functionx.com/visualc/gdi/gdicoord.htm)

[Zooming using Viewport](https://www.codeproject.com/Questions/605822/ZoomingplususingplusViewport)

[Menus and Icons](http://www.winprog.org/tutorial/menus.html)
