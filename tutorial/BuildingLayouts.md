# Building Layouts

*Macroid* comes with concise and easy to use layout [bricks](../guide/Bricks.html):

* Layouts: `l[LinearLayout](...)`
* Widgets: `w[TextView](...)`

Our example layout for this tutorial will consist of a button
that displays a text box with a greeting. The first sketch looks like this:

```scala
l[LinearLayout](
  w[Button],
  w[TextView]
)
```

We’ll customize these bricks in a moment, but first let’s include them into
some real Android code:

```scala
// import macroid stuff
import macroid._
import macroid.FullDsl._

// include implicit contexts
class GreetingActivity extends Activity with Contexts[Activity] {
  override def onCreate(savedInstanceState: Bundle) = {
    super.onCreate(savedInstanceState)

    // the layout goes here
    setContentView {
      getUi {
        l[LinearLayout](
          w[Button],
          w[TextView]
        )
      }
    }
  }
}
```

By the way, a really nice thing about *Macroid* is its emphasis on composability.
Unlike Android XML,
we can declare the widgets wherever we want and stack them together as needed:

```scala
// ActivityContext is an Android Context obtained from an Activity
import macroid.ActivityContext

// A module with layouts
object OurLayouts {
  def layout1(implicit ctx: ActivityContext) =
    l[LinearLayout](
      w[TextView],
      w[ImageView],
      w[Button]
    )

  def layout2(implicit ctx: ActivityContext) =
    l[FrameLayout](
      w[ProgressBar]
    )

  def layout3(implicit ctx: ActivityContext) =
    l[FrameLayout](
      layout1,
      layout2
    )
}
```

And now let’s proceed to tweaking our widgets.
