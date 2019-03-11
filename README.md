# PropMapper
Property mapper for .NET. Flat and basic, but **VERY FAST**.

## Usage

Just one line of code:

```cs
DestType destObject = PropMapper<SourceType, DestType>.From(srcObj);
```

or

```cs
var srcObj = new SourceType();
var destObject = new DestType();
PropMapper<SourceType, DestType>.CopyTo(srcObj, destObject);
```

## Benchmarks

Mapping a simple object with 50 properties, over 100k iterations. And I even cached Automapper's `config` which is kinda unfair (but without caching it just times out)

Results:

| Mapper  | Results |
| ------------- | ------------- |
| Automapper   | 335ms  |
| **PropMapper**   | **25ms**  |
| Manual code  | 10ms  |

Object type if you insist

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

PropMapper is more than 10 times faster.

## Limitations 

The project does not support nested properties at the moment, only first level properties.

## Under the hood

We use compiled Expression trees, created in the static constructor and cached ina var, which makes it really fast.

## Use case

```cs
public class Person
{
	public string FirstName { get; set; }
	public string LastName { get; set; }
}
public class Employee : Person
{
	public string Title { get; set; }
	
	public Employee(Person person)
	{
		PropMapper<Person, Employee>.CopyTo(person, this);
	}
}
```

# Nuget? Unit tests?

Currently it's just one C# file, Nuget, tests and benchmarks coming later. The tool is in heavy use in other projects of ours, so it's regularly unit-tested anyway.
