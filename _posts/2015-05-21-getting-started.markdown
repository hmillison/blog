---
layout: post
title:  "Getting Started"
date:   2015-05-21 11:01:57
categories:
---

<img class="photo" id="react-logo" src="/blog/images/Reactjs_logo.png" alt="A picture of my beautiful face" title="A picture of my beautiful face">
I often hear people talk about how they want to learn how to program, but invariably they give some reason for why they can’t do it. Whenever I hear this, I want to shake them and say, “YOU CAN TEACH YOURSELF!” Programming and software development as a whole has an assortment of resources online due to the fact that people who know how to do it are always on their computer. It seems that programming is slowly becoming a skill that could be essential to our work as many other subjects that are taught in high school. In this current era where millennials struggle to find gainful employment while software engineers are commanding absurd salaries in Silicon Valley, it is fortunate that programming is something that can be easily self-taught.

Unfortunately, programming is not something in a book that you can just reach and suddenly you are the next Mark Zuckerberg. It requires you to spend time trying to create things and going through the frustration of getting everything to work as expected. This time spent googling away is essential to becoming a skilled software developer. I have learned after many hours of fruitlessly searching for help to a problem that I had in a project that the answer was right under my nose the whole time. This road to learning how to ask the right questions when confused is one of the greatest skills to acquire in the confusing road of learning to program.

I maybe getting ahead of myself here. As a programmer who learned through school and by teaching myself, I want to illustrate the path of going from being completely with a technology (or in your case, programming as a whole) to being able to build awesome things with it. The first roadblock that we both face, just like when you have a big essay due, is getting started.

Take a look at this snippet of code below:

{% highlight JavaScript %}
var CommentBox = React.createClass({
  loadCommentsFromServer: function() {
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      cache: false,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  handleCommentSubmit: function(comment) {
    var comments = this.state.data;
    var newComments = comments.concat([comment]);
    this.setState({data: newComments});
    $.ajax({
      url: this.props.url,
      dataType: 'json',
      type: 'POST',
      data: comment,
      success: function(data) {
        this.setState({data: data});
      }.bind(this),
      error: function(xhr, status, err) {
        console.error(this.props.url, status, err.toString());
      }.bind(this)
    });
  },
  getInitialState: function() {
    return {data: []};
  },
  componentDidMount: function() {
    this.loadCommentsFromServer();
    setInterval(this.loadCommentsFromServer, this.props.pollInterval);
  },
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.state.data} />
        <CommentForm onCommentSubmit={this.handleCommentSubmit} />
      </div>
    );
  }
});
{% endhighlight %}

This may look completely incomprehensible to you and me. It is an example from the tutorial on [React], a Javascript library for creating user interfaces created by Facebook. I want to learn this to continue to keep up with the cutting edge technologies that are available in the constantly evolving world of web development.

For the non-programmer readers out there, I apologize for the difficulty to follow so let me attempt to break down how web development works! Every website has what’s called a Front End and Back End. The Front End consists of everything you see and the various things on the page you can interact with.

We can breakdown the Front End into three main technologies: HTML, CSS, and Javascript. HTML is the structure of the webpage and the actual content that you see. CSS takes the HTML and makes it look pretty, if there was no CSS it would just be black text on a white background (like [Berkshire Hathaway’s website][Berkshire]). Javascript is everything that makes the page interactive. It can take a boring website and turn it into a web application.

The Back End is how all the data is sent back and from the user to the server. Whenever you click a link or access a web page, it is accessing the Back End. When you create a new comment or like a post on Facebook, the Front End is sending that information to the Back End so it is recorded for everyone. The Back End is ultimately how a website like Facebook keeps track of all the different data that the user has and interacts with. As a user, it seems more like a black box where your actions go in and something comes out without you knowing what is going on in between.

Now back to React, where does that fit into all of this? React is a library for Javascript. Basically, it is meant to provide a new way to structure your interface and make it more dynamic without overcomplicating it. Facebook’s Engineering team created this library in order to make the immense complexity of their application easier to manage. As you can imagine, there are numerous things that are constantly changing when you access Facebook and it was important for there to be a better way to manage all of that changing information. React is open source, which means anyone can see the code used to create it and contribute changes if they want to. It is currently being adopted by developers working on the Front End throughout the world due to it’s ease at turning confusingly structured web applications into something that is more manageable.

I am excited to have you on this journey with me, next week I will discuss the frustration of trying to figure out how to build an application with a technology when you are just beginning the process of learning it.

[React]:      https://facebook.github.io/react/index.html
[Berkshire]:   http://www.berkshirehathaway.com
