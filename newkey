@echo off

SETLOCAL

set downloaddir=%userprofile%\Downloads
set destdir=%userprofile%\Putty
set filename=key.ppk

goto main

:test
echo %downloaddir%
echo %destdir%
echo %filename%
echo %downloaddir%\%filename%
goto end

:: after download new ppk file, copy to specified location overwriting existing
:: or provide a reminder to download by deleting after copy or move the file
:: no file in source dir == did not download today/when needed

:main
if exist %downloaddir%\%filename% (
  forfiles /p "%downloaddir%" /s /m %filename% /D 0 /C "cmd /c dir @file"
  forfiles /p "%downloaddir%" /s /m %filename% /D 0 /C "cmd /c move /Y %filename% %destdir%\%filename%"

  if exist %downloaddir%\%filename% (
    echo %filename% is older than today and was not moved
    echo but will now be deleted
    forfiles /p "%downloaddir%" /s /m %filename% /D -1 /C "cmd /c echo @file"
    forfiles /p "%downloaddir%" /s /m %filename% /D -1 /C "cmd /c del /q @file"
    ) else (
      echo %filename% has been moved to %destdir% !
    )
    goto cleanup
    ) else  (
      echo Please download a new %filename%
      goto cleanup
)

:cleanup
:: For any other type of key files, or older ppk that didn't get moved
:: older than (last modified longer ago than, due to windows limitations)
:: seek and destroy

if exist %downloaddir%\*.rdp (
  echo Cleaning up old rdp files in %downloaddir%
  forfiles /p "%downloaddir%" /s /m *.rdp /D -1 /C "cmd /c echo @file"
  forfiles /p "%downloaddir%" /s /m *.rdp /D -1 /C "cmd /c del /q @file"
)

if exist %downloaddir%\*.openssh (
  echo Cleaning up old openssh files in %downloaddir%
  forfiles /p "%downloaddir%" /s /m *.openssh /D -1 /C "cmd /c echo @file"
  forfiles /p "%downloaddir%" /s /m *.openssh /D -1 /C "cmd /c del /q @file"
)

if exist %downloaddir%\*.pem (
  echo Cleaning up old pem files in %downloaddir%
  forfiles /p "%downloaddir%" /s /m *.pem /D -1 /C "cmd /c echo @file"
  forfiles /p "%downloaddir%" /s /m *.pem /D -1 /C "cmd /c del /q @file"
)

if exist %downloaddir%\*.ppk (
  echo Cleaning up old ppk files in %downloaddir%
  forfiles /p "%downloaddir%" /s /m *.ppk /D -1 /C "cmd /c echo @file"
  forfiles /p "%downloaddir%" /s /m *.ppk /D -1 /C "cmd /c del /q @file"
)
goto end

:end
pause
ENDLOCAL
Exit
