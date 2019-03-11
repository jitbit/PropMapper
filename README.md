# PropMapper
Property mapper for .NET. Flat and basic, but VERY FAST.

## Banchmarks

Mapping a simple object with 50 properties:

```cs
public class Tester
{
	public string prop1 { get; set; }
	public string prop2 { get; set; }
	public string prop3 { get; set; }
	public int iprop1 { get; set; }
	//etc. 50 times
}
```

100k iterations

Results:

| Mapper  | Results |
| ------------- | ------------- |
| Automapper   | 335ms  |
| **PropMapper**   | 25ms  |
| Manual code  | 10ms  |

PropMapper is more than 10 times faster.

The project does not support nested properties at the moment, only first level properties.
