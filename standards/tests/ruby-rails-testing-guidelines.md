# Ruby/Rails Testing Guidelines

When testing code written in Ruby on Rails, there are some scenarios or points of confusion that we encounter from time to time. Here are some guidelines we follow to make testing more effective.

## Avoid controller specs

Controller specs are used to test controllers specifically the templates rendered, instance variables passed, or redirects by simulating a controller object. They are no longer recommended by RSpec (use request specs instead) and should only be used if dealing with an old project with existing controller tests.

```ruby
RSpec.describe UsersController, type: :controller do
  describe "GET index" do
    it "assigns @users" do
      user = User.create
      get :index
      expect(assigns(:team)).to eq([team])
    end

    it "renders the index template" do
      get :index
      expect(response).to render_template("index")
    end
  end
end
```

## Prefer request specs over controller specs

Request specs test controllers as if doing an actual request. These specs tend to be slow because they deal with rendering full pages and when overused can result in a slow running CI. Aside from that request specs may overlap with end-to-end testing (also called feature specs) which is usually handled with different tools (e.g. Ghost Inspector, Cypress). Use request specs to test controllers in the following scenarios:
- ✅ routing (e.g. does it redirect, can a certain user access the page )
  ```ruby
  RSpec.describe "PostsController", type: :request do
    describe "GET #new" do
      it "redirects to dashboard if user is not active" do
        get new_posts_path
        expect(response).to redirect_to(dashboard_path)
      end
    end
  end
  ```
- ❌ Rendering of elements on the page (more for end-to-end testing)
  ```ruby
  RSpec.describe "UsersController", type: :request do
    describe "GET #users" do
      it "renders the user" do
        user = User.create(name: “Test user”)
        get users_path
        expect(response.body).to include(“Test user”)
      end
    end
  end
  ```
- ❌ controller action logic (Basic actions are straightforward enough and don't need to be tested. If your actions have complex logic better to extract to a service and test that)
  ```ruby
    RSpec.describe "ArticlesController", type: :request do
      describe "POST #create" do
        it "creates an article" do
          post article_path(params: { article: { title: "Test Article", body: "This is the content" } })
          article = Article.last
          expect(article.title).to eq "Test Article"
        end
      end
    end
  ```

## Use request specs to test API controllers

Request specs are more recommended for API controllers since these usually just return JSON format responses instead of entire pages. Use to test the following:
- ✅ response status and body
  ```ruby
    RSpec.describe "Api::ArticlesController", type: :request do
      describe "POST #create" do
        let(:user) { User.create(name: “Test user”) }
        let(:headers) { "Authorization" => user.jwt_encode }
        let(:params) { { title: "Test Article", body: "This is the content" } }

        it "creates an article" do
          post "/api/articles", headers: headers, params: params
          expect(response.status).to eq 201
          expect(JSON.parse(response.body)["data"]["attributes"]["body"]).to eq "This is the content"
        end
      end
    end
  ```
- ❌ API logic (Should focus on response instead of controller logic. If complex logic, extract to a service and test that)
  ```ruby
    RSpec.describe "Api::ArticlesController", type: :request do
      describe "POST #create" do
        let(:user) { User.create(name: “Test user”) }
        let(:headers) { "Authorization" => user.jwt_encode }
        let(:params) { { title: "Test Article", body: "This is the content" } }

        it "creates an article" do
          post "/api/articles", headers: headers, params: params
          article = Article.last
          expect(article.title).to eq "Test Article"
        end
      end
    end
  ```
