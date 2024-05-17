## Internal notes on reusing hbfwh-FOC.

BLDC_controller and BLDC_controller_data are generated code so there be dragons!

bldc.c is a shim between the generated Symlink model and underlying stm32 host device with everything being done inside DMA1_Channel1_IRQHandler which is being triggered at around [100KHz in original commit, but latest code is 20KHz]    and for the most part copies various extern values to and from models parameter block before and after turning the crank via BLDC_controller_step(..)
before making adjustments to the pwm values.

model has variables for mechanical and electrical angles (need to set a flag variable to force there use instead of computed values)..

#### ABORT - EFerum firmware is to be phased out of project ASAP
Only utility to be gained is as a known working hardware configuration so will stay as the framework for testing our own 'BLDC_controller' equivalent code (far above parity since we are including IPD and sensorless) but then will be removed in favour of a minimal configuration generated from scratch using ST tools.