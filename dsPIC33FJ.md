

### Include files and spin inside main infinitely

```
#include <xc.h>           // will choose the correct include for every controller inside
#include <p33Fxxxx.h>
#define FCY 12800000UL 
#include <libpic30.h>

#include "led.h"
...
int main(){
    while(1);
}
```

### Using LCD

```
...
#include "lcd.h"
int main(){
    lcd_initialize(); // important
	  lcd_clear(); // Clear the Screen and reset the cursor
    lcd_locate(0, 0);
    // Print macro
    lcd_printf("Hello World");
    // Stop
    while(1);
}
```



### Common issues

- "Build chain for XC16 not found..."
-> go to Tools/Options/Embedded/Build Tools -> "scan for build tools" -> "apply" -> close and reopen current project

