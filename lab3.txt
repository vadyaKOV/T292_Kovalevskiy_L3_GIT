// //callbacks
function getPostsWithCallback(callback){
    const xhr = new XMLHttpRequest();
    xhr.open('GET', 'https://jsonplaceholder.typicode.com/posts');
    xhr.onload = () => {
        const data = JSON.parse(xhr.responseText);
        const sorted = data.sort((a,b) => b.title.length - a.title.length);
        callback(sorted);
    };
    xhr.send();
}

function getCommentsWithCallback(callback){
    const xhr = new XMLHttpRequest();
    xhr.open('GET', 'https://jsonplaceholder.typicode.com/comments');
    xhr.onload = () => {
        const data = JSON.parse(xhr.responseText);
        const sorted = data.sort((a,b) => b.title.length - a.title.length);
        callback(sorted);
    };
    xhr.send();
}

//promises
function getUsersWithPromise(){
    return fetch('https://jsonplaceholder.typicode.com/users')
    .then(res => res.json())
    .then(data => data.map(({id, name, username, email, phone}) => ({id, name, username, email, phone})));
}

function getTodosWithPromise(){
    return fetch('https://jsonplaceholder.typicode.com/todos')
    .then(res => res.json())
    .then(data => data.filter(todo => !todo.completed));
}

//async await
async function getPostsAsync(){
    const res = await fetch('https://jsonplaceholder.typicode.com/posts');
    const data = await res.json();
    return data.sort((a, b) => b.title.length - a.title.length);
}

async function getCommentsAsync(){
    const res = await fetch('https://jsonplaceholder.typicode.com/comments');
    const data = await res.json();
    return data.sort((a, b) => a.name.localeCompare(b.name));
}

async function getUsersAsync(){
    const res = await fetch('https://jsonplaceholder.typicode.com/users');
    const data = await res.json();
    return data.map(({id, name, username, email, phone}) => ({id, name, username, email, phone}));
}

async function getTodosAsync(){
    const res = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await res.json();
    return data.filter(todo => !todo.completed);
}

async function runAsyncFunctions() {
    const posts = await getPostsAsync();
  console.log('Posts (async):', posts);

  const comments = await getCommentsAsync();
  console.log('Comments (async):', comments);

  const users = await getUsersAsync();
  console.log('Users (async):', users);

  const todos = await getTodosAsync();
  console.log('Todos (async):', todos);
}

//executes
getPostsWithCallback((sorted) => {
    console.log("Posts (callback): ", sorted);
});

getCommentsWithCallback((sorted) => {
    console.log("Comments (callback): ", sorted);
});

getUsersWithPromise().then(users => {
    console.log("Users (promise): ", users);
});

getTodosWithPromise().then(todos => {
    console.log("Todos (promise): ", todos);
});