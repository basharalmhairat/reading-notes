## RecyclerView

### Create dynamic lists with RecyclerView  : 

RecyclerView makes it easy to efficiently display large sets of data. You supply the data and define how each item looks, and the RecyclerView library dynamically creates the elements when they're needed.

As the name implies, RecyclerView recycles those individual elements.
When an item scrolls off the screen, RecyclerView doesn't destroy its view. 
Instead, RecyclerView reuses the view for new items that have scrolled onscreen. This reuse vastly improves performance,
improving your app's responsiveness and reducing power consumption.

![image](https://user-images.githubusercontent.com/97823170/167121757-59d049b6-b3a5-4399-b7db-d6d78180bb9d.png)

Note: Besides being the name of the class, RecyclerView is also the name of the library. In this page,
RecyclerView in code font always means the class in the RecyclerView library.

### Key classes:

Several different classes work together to build your dynamic list.

RecyclerView is the ViewGroup that contains the views corresponding to your data. It's a view itself, so you add RecyclerView into your layout the way you would add any other UI element.

Each individual element in the list is defined by a view holder object. When the view holder is created, it doesn't have any data associated with it. After the view holder is created, the RecyclerView binds it to its data. You define the view holder by extending RecyclerView.ViewHolder.

The RecyclerView requests those views, and binds the views to their data, by calling methods in the adapter. You define the adapter by extending RecyclerView.Adapter.

The layout manager arranges the individual elements in your list.
You can use one of the layout managers provided by the RecyclerView library,
or you can define your own. Layout managers are all based on the library's LayoutManager abstract class.

### Steps for implementing your RecyclerView:

![image](https://user-images.githubusercontent.com/97823170/167121702-7a223210-ef0b-4368-801d-304c5590d7eb.png)

If you're going to use RecyclerView, there are a few things you need to do. They'll be discussed in detail in the following sections.

First of all, decide what the list or grid is going to look like. Ordinarily you'll be able to use one of the RecyclerView library's standard layout managers.

Design how each element in the list is going to look and behave. Based on this design, extend the ViewHolder class. Your version of ViewHolder provides all the functionality for your list items. Your view holder is a wrapper around a View, and that view is managed by RecyclerView.

Define the Adapter that associates your data with the ViewHolder views.
### Plan your layout:

The items in your RecyclerView are arranged by a LayoutManager class. The RecyclerView library provides three layout managers, which handle the most common layout situations:

LinearLayoutManager arranges the items in a one-dimensional list.
GridLayoutManager arranges all items in a two-dimensional grid:
If the grid is arranged vertically, GridLayoutManager tries to make all the elements in each row have the same width and height, but different rows can have different heights.
If the grid is arranged horizontally, GridLayoutManager tries to make all the elements in each column have the same width and height, but different columns can have different widths.
StaggeredGridLayoutManager is similar to GridLayoutManager, but it does not require that items in a row have the same height (for vertical grids) or items in the same column have the same width (for horizontal grids). The result is that the items in a row or column can end up offset from each other.
You'll also need to design the layout of the individual items.
You'll need this layout when you design the view holder, as described in the next section.

![image](https://user-images.githubusercontent.com/97823170/167121654-151f59ad-6768-49f5-8fab-f2f4d84d4871.png)

### Implementing your adapter and view holder:

Once you've determined your layout, you need to implement your Adapter and ViewHolder. These two classes work together to define how your data is displayed. The ViewHolder is a wrapper around a View that contains the layout for an individual item in the list. The Adapter creates ViewHolder objects as needed, and also sets the data for those views. The process of associating views to their data is called binding.

When you define your adapter, you need to override three key methods:

onCreateViewHolder(): RecyclerView calls this method whenever it needs to create a new ViewHolder. The method creates and initializes the ViewHolder and its associated View, but does not fill in the view's contents—the ViewHolder has not yet been bound to specific data.

onBindViewHolder(): RecyclerView calls this method to associate a ViewHolder with data. The method fetches the appropriate data and uses the data to fill in the view holder's layout. For example, if the RecyclerView displays a list of names, the method might find the appropriate name in the list and fill in the view holder's TextView widget.

getItemCount(): RecyclerView calls this method to get the size of the data set. For example, in an address book app, this might be the total number of addresses. RecyclerView uses this to determine when there are no more items that can be displayed.

Here's a typical example of a simple adapter with a nested ViewHolder that displays a list of data. In this case, the RecyclerView displays a simple list of text elements. The adapter is passed an array of strings, containing the text for the ViewHolder elements.
