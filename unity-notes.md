# UNITY NOTES

## Classes and Methods:

**GetComponent<T>():**	This allows us to retrieve the component of type T when the script is attached to a GameObject.

Types covered in lecture
- Rigidbody
- AddForce(Vector3, ForceMode) - This is a physics method can be applied to a Rigidbody.
- AudioSource

**Instantiate(Object)**
:	This will allow us to clone the object.
```csharp
public class SpawnPoint : MonoBehaviour {

	public GameObject ObjectToSpawn;
	public Transform SpawnLocation;

	void Start() {
		InvokeRepeating ("GenerateObject", 0f, 2f);
	}

	public void GenerateObject() {
		Instantiate (ObjectToSpawn, SpawnLocation.position, transform.rotation);
	}
}
```
**Delete(Object)**
:	This script is attached to an empty game object and will delete the cloned object from above

```csharp
public class ObjectDelete : MonoBehaviour {

	public string DeleteTag = string.Empty;

	// Use this for initialization
	void Start() {
		InvokeRepeating("DeleteObjectsOfTag", 0f, 2f);
	}

	public void DeleteObjectsOfTag() {
		GameObject[] MyObjects = GameObject.FindGameObjectsWithTag(DeleteTag);

		for (int i = 0; i < MyObjects.Length; i++) {
			Destroy(MyObjects[i]);
		}
	}
}
```
**Camera.ScreenPointToRay(Input)**
:	This will draw a ray based on where the input is. For example if the input is Input.mousePosition, then it will create a ray to everything that the mouse will mouse point

Color.* = This allows you to get a color.

Input.* = This allows you to get input from your peripherals.

Quaterion.* = Allows us to construct quaterions.
- Quaterion.Euler = gives us a rotation in this order: Z-axis, X-axis, then Y-axis.
- Quaterion.FromToRotation = give it 2 directions (fromDirection & toDirection) and it will tell how to get to those directions
- Quaterion.AngleAxis = define an axis and how many degrees to rotate around that access.
- Quaterion.LookRotation = Creates a rotation with the specified forward and upwards directions.

## Physics

**FixedUpdate():** In Unity, we have Update that is done every frame and then we have FixedUpdate(), which is done only after a fixed amount time. This timing can be found in {Edit --> Project Setting --> Time} under "Fixed Timestap." 

Now FixedUpdate() happens before Update() in the execution order but it can occur several times in one frame for slow frame rates or can not be executed at all in high frame rates.

When applying movement calculations inside FixedUpdate(), you do not need to multiply your values by Time.deltaTime. This is because FixedUpdate() is called on a reliable timer, independent of the frame rate.

Ex:
```csharp
void FixedUpdate () {
	Rigidbody rb = GetComponent<Rigidbody>();
	rb.AddForce(new Vector3(0,0,force)); // Note: You have to apply this to a Rigidbody.
}
```
## Distances and Loops:

```csharp
public class MoveToWayPoint : MonoBehaviour {

	private GameObject[] Waypoints;
	private NavMeshAgent Agent;

	// Use this for initialization
	void Start() {
		Waypoints = GameObject.FindGameObjectsWithTag("Respawn");
		NA = GetComponent<NavMeshAgent>();
		GameObject Nearest = GetNearestWaypoint();
		NA.SetDestination(Nearest.transform.position);
	}

	public GameObject GetNearestWaypoint() {
		GameObject Nearest = Waypoints[0];
		float NearestDistance = Vector3.Distance(transform.position, Nearest.transform.position);

		foreach (GameObject W in Waypoints) {
			float Distance = Vector3.Distance(transform.position, W.transform.position);

			if (Distance < NearestDistance) {
				Nearest = W;
				NearestDistance = Distance;
			}
		}

		return Nearest;
	}
}
```
## Coroutines:
Functions that run asynchronously and in parallel.
```csharp
	public class Mover : MonoBehaviour {
		void Start() {
			StartCoroutine(Move());
		}

		public IEnumerator Move() {
			while (true) {
				print("Frame Happened. Time: " + Time.time);
				yield return null;
			}
		}
	}
```
## Animation:

```csharp
public class AnimTrigger : MonoBehaviour 
{
	public Animator TargetAnimator = null;
	public string TriggerName = string.Empty;

	void OnTriggerEnter(Collider Col)
	{
		TargetAnimator.SetTrigger (TriggerName);
	}
}
```
## Creating a NavMesh
To create the Player as a NavMeshAgent:

1. Go to Window --> AI --> Navigation.
2. On the "Bake" tab, select the default settings and click "Bake".
3. Go to the Player object, add a "NavMeshAgent" component.
