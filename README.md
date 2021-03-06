# Week 3 Comprehensive Assessment

Fork this repository, update this file to include your answers, and submit a pull request. You may refer to any notes, past projects, or external resources you want. The questions do not have to be completed in order.

### Models

1. I'm creating an app to keep track of bunnies. I already have a `bunnies` table, but I want to create a migration to add a "weight" column to it. What command should I run in my terminal to get started?

rails g migration AddWeightColumnToBunnies

2. I just realized I misspelled the "weight" column in my migration, but I already ran `rake db:migrate`. What should I do to fix this? (give exact steps and/or commands to run)

Create a new migration with rails g migration ChangeWeightColumn
Inside the migration change method, add the following:
remove_column :bunnies, :waieght, :numeric
add_column :bunnies, :weight, :numeric

(Referred to tuesday's notes)

3. My app has a `Bunny` model, and I want to find bunnies whose `color` attribute is `'white'`, sorted by their `name` attribute. What code should I write to do that?

Bunny.where(color: 'white').order(:name)

(Referred to tuesday's notes)

4. Now I want to find the specific bunny whose name is `'George'` (names are unique, so there should be only one).

Bunny.find_by(name: "George")

5. I want to make sure nobunny, er, I mean nobody, can create a bunny without a name. What code should I add to my `Bunny` model to validate this?

validates :name, presence: true

### Controllers

1. My app is telling me there's an error in the `BunniesController`. What directory and filename should I look in?

app/controllers/bunnies_controller

2. I'm in the `show` action of my `BunniesController` and I have the ID of a specific bunny in `params[:id]`. What line should I type to find the bunny with the correct ID, and assign it to a variable that my view can access?

@bunny = Bunnies.find(params[:id])


3. I tried to update a bunny with the code `bunny.update(params[:bunny])`, but it gave me a "forbidden attributes error". Why is it telling me this, and what should I do (broadly speaking, no exact code needed) to fix the problem?

You haven't permitted the :bunny attribute in your params. In your method called "bunny_params", make sure the :bunny attribute is in the array of permitted attributes. Then, instead of using bunny.update(params[:bunny]), use bunny.update(bunny_params)

(For the syntax in here, I referred to the crud demo files from yesterday)

4. When I create or update a bunny in my controller, how can I find out whether the bunny saved successfully?
In the rails console, type bunny.persists? -- if it saved, it will return true
Alternatively, look for the bunny in your index.

5. Assuming my bunny saved successfully, what code should I write to redirect the user to the "show" page for the bunny?

if bunny.save
  redirect_to bunny_path
end

(Same as #3 -- I referred to yesterday's demo for the syntax)

### Routes/Views

1. What line should I add to `config/routes.rb` to create a complete set of RESTful routes for a "bunnies" resource?

resource :bunnies


2. My app is telling me there's an error in the "show" view for bunnies. What directory and filename would that be located in?

app/views/bunnies/show.html.erb

3. I'm in the `index.html.erb` view and I've assigned a variable `@bunnies` to a collection of all my bunnies. What HTML/ERB code should I write to create an unordered list that shows each bunny's `name` attribute?

<ul>
  <%= @bunnies.each do |bunny|%>
    <li><%= bunny.name %></li>
  <% end %>
</ul>

4. In one of my views, I want to create a link to the "show" path for a specific bunny that I have stored in the variable `bunny`. `rake routes` tells me that I have a standard `bunny_path` helper available. How do I create this link?

<%= link_to "See this bunny", bunny_path %>

5. I've created a view partial called `_form.html.erb` and I want to render this partial into my "new" view. What HTML/ERB code should I write to do this?

<%= render 'form', bunny: @bunny %>

(Referred to my bookmarkr homework for exact syntax)


