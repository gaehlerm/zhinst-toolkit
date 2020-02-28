# Class Diagram


```mermaid

classDiagram

    hdawg --|> Device
    hdawg *-- awg
    uhfqa --|> Device
    uhfqa *-- awg
    uhfli --|> Device
    uhfli *-- awg
    pqsc --|> Device
    BaseController *-- Device
    BaseController *-- ZIDeviceConnection
    ZIDeviceConnection --> ziPython
    BaseController *-- InstrumentConfiguration
    AWGController --|> BaseController
    AWGController *-- Compiler
    PQSCController --|> BaseController
    LIController --|> BaseController
    Compiler *-- SequenceProgram
    SequenceProgram *-- Sequence
    SimpleSequence --|> Sequence
    RabiSequence --|> Sequence
    T1Sequence --|> Sequence
    T2Sequence --|> T1Sequence
    Sequence --> SeqCommands
    AWGCore_for_UHFQA --|> AWGCore
    AWGCore_for_HDAWG --|> AWGCore
    AWGCore .. AWGController
    HDAWG *-- AWGController
    UHFQA *-- AWGController
    HDAWG *-- AWGCore_for_HDAWG
    UHFQA *-- AWGCore_for_UHFQA
    UHFQA *-- ReadoutChannel
    UHFLI *-- LIController
    PQSC *-- PQSCController
    MultiDeviceController *-- HDAWG
    MultiDeviceController *-- UHFQA
    MultiDeviceController *-- UHFLI
    MultiDeviceController *-- PQSC
    MultiDeviceController *-- ZIDeviceConnection
    MultiDeviceController *-- InstrumentConfiguration
    

    
    class Device{
        +name
        +serial
        +interface
    }
    class awg{
        +parent
        +index
        +waveforms
        +program
    }
    class hdawg{
        +awgs
    }
    class uhfqa{
        +awg
    }
    class pqsc
    class uhfli{
        +awg
    }
    class BaseController{
        -connection
        -config
        -device
        +setup()
        +connect_device()
        +set()
        +get()
        +get_nodetree()  
    }
    class ZIDeviceConnection{
        -details
        -daq
        -awg_module
        +connect()
        +connect_device()
        +set()
        +get()
        +list_nodes()  
    }
    class InstrumentConfiguration{
        +api_config
        +instrument_config
    }
    class AWGController{
        -compiler
        +awg_compile()
        +awg_run()
        +awg_stop()
        +awg_queue_waveform()
        +awg_set_sequence_parameter()
    }
    class PQSCController
    class LIController
    class Compiler{
        -sequences
        -device
        +add_device()
        +set_parameter()
        +get_program()
    }
    class SequenceProgram{
        -sequence_type
        -sequence
    }
    class Sequence
    class SimpleSequence
    class RabiSequence
    class T1Sequence
    class T2Sequence
    class SeqCommands
    class AWGCore{
        -parent
        -index
        +compile()
        +run()
        +stop()
        +queue_waveform()
        +set_sequence_params()
    }
    class HDAWG{
        -name
        -controller
        +awgs
        +get()
        +set()
    }
    class UHFQA{
        -name
        -controller
        +awg
        +channels
        +get()
        +set()
    }
    class UHFLI{
        -name
        -controller
        +awg
        +get()
        +set()
    }
    class PQSC{
        -name
        -controller
        +get()
        +set()
    }
    class ReadoutChannel{
        +enabled
        +rotation
        +threshold
        +enable()
        +disable()
    }

    class AWGCore_for_HDAWG{
        +output
        +iq_modulation
        +mod_freq
        +mod_phase
        +mod_gains
        -apply_sequence_settings()
    }

    class AWGCore_for_UHFQA{
        +output
        +mod_gains
        +update_readout_params()
        -apply_sequence_settings()
    }
    class MultiDeviceController{
        -shared_connection
        -config
        +hdawgs
        +uhfqas
        +pqsc
        +setup()
        +connect_device()
    }

```