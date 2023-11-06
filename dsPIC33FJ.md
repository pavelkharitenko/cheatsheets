

### Include files and spin inside main infinitely

```
#include <xc.h>			// will choose the correct include for every controller inside
#include <p33Fxxxx.h>		// Enables macros
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
    lcd_printf("Counter = %u", i_counter); // u for print unsigned 
    // Stop
    while(1);
}
```

### Registers

- Timer 1: Used as the counter for the real clock, can be prescaled
```
void initTimer1(unsigned int period){
	T1CON = 0; 		// loads binary 00..0 into T1CON register, sets all digits to 0
	T1CONbits.TON = 0; 	// sets single bits TON of register T1CON through Xbits.Y. Here 0 means disable timer 
	T1CONbits.TCKPS = 0b10; // Set prescaler to 2 (or binary 10), to scale by 1/64 
...
```

### Input/Output settings

The pins of ports A-G can be set as I/O and controlled with registers **TRIS**, **PORT** & **LAT**:

- TRISx: Set data direction of pins at Port X, a 1 is input
```
TRISAbits.TRISA10 = 0; 		// set pin 10 of port A as output
```

- PORTx: Read or write to respective I/O port: 
```
PORTAbits.RA10 = 1; 		// set pin RA10 to high (if configured as output pin)
```

- LAT: Not important for lab exercise.

Example of outputting a one on port A:
```
CLEARBIT(TRISDbits.TRISD6);	// sets pin 6 or port D to 0, means as output
SETBIT(PORTDbits.PORTD6);	// write 1 to pin 6 on port D, means output HIGH
```
A Nop() operation is needed, when changing, reading or writing to pins.
Both use CLEAR/SET-BIT macro that already includes necessary Nop() command.


### Using available LEDs
Five pins, 0, 4, 5, 9 & 10, of Port A are already connected to LEDs. Macros can be used:
```
CLEARBIT(TRISAbits.TRISA10); //sets LED4 to output
Nop(); // necessary
SETLED(PORTAbits.RA10); //turn on LED4
CLEARLED(PORTAbits.RA10); //turn off LED4
// these two macros don't need Nop()
```

### Interrupts

Triggered by a hardware event, to execute another code segment, deviating from current program.

- Synchronous Interrupts: issued by CPU control unit betweeen instructions. E.g. Kernel function needs to be called at some point in the program.

- Asynchronous Interrupts: issued by other hardware components. E.g. connected device like printer sends ready signal.

The dsPIC33F interrupt model:
```
1. save program counter and status bits 
	2. set interrupt priority in bits 0,1,2 of IPL register (other lower or equal interrupts are blocked)
		3. get ISR address from Interrupt Vector Table
			4. push used registers on stack
				5. handle interrupts
			6. pop used registers
	7. RETFIE (terminate interrupt and remove IPL)
8. pop PC and status bits (sb contain programs original priority)
```

Interrupt Vector Table stores what is to execute when certain ISR is called
   
### Common issues

- "Build chain for XC16 not found..."
-> go to Tools/Options/Embedded/Build Tools -> "scan for build tools" -> "apply" -> close and reopen current project

