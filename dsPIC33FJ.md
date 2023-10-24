

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
    lcd_initialize();		// important
    lcd_clear(); 		// Clear the Screen and reset the cursor
    lcd_locate(0, 0);
    
    lcd_printf("Hello World");  // Print macro
    // Stop
    while(1);
}
```

### Registers

- Timer 1: Used as the counter for the real clock, can be prescaled
```
void initTimer1(unsigned int period){
	T1CON = 0; 		// loads binary 00..0 into T1CON register, sets all digits to 0
	T1CONbits.TON = 0; 	// sets single part TON of register T1CON through Xbits.Y. Here 0 means disable timer 
	T1CONbits.TCKPS = 0b10; // Set prescaler to 2 (or binary 10), to scale by 1/64 
...
```

### Common issues

- "Build chain for XC16 not found..."
-> go to Tools/Options/Embedded/Build Tools -> "scan for build tools" -> "apply" -> close and reopen current project

