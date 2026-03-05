```java
public class Book {
    private String Title;
    private String Author;
    private String Publisher;
    private String publishDate;

    public void setTitle(String Title) {
        this.Title = Title;
    }

    public String getTitle() {
        return Title;
    }

    public void setAuthor(String Author) {
        this.Author = Author;
    }

    public String getAuthor() {
        return Author;
    }

    public void setPublisher(String Publisher) {
        this.Publisher = Publisher;
    }

    public String getPublisher() {
        return Publisher;
    }

    public void setPublishDate(String publishDate) {
        this.publishDate = publishDate;
    }

    public String getPublishDate() {
        return publishDate;
    }

    public void displayInfo() {
        System.out.println("Book Information:\n Book Title : " + getTitle() + "\n Author: " + getAuthor() + "\n Publisher: " + getPublisher() + "\n Publication Date: " + getPublishDate());
    }
}
public class Encyclopedia extends Book{
    private String Edition;
    private int Pages;

    public void setEdition(String Edition){
        this.Edition=Edition;
    }
    public String getEdition(){
        return Edition;
    }
    public void setPages(int Pages){
        this.Pages=Pages;
    }
    public int getPages(){
        return Pages;
    }
@Override
public void displayInfo(){    //use getter methods because the variables are private. Can use protected to get them directly.
    System.out.println("Book Information:\n Book Title : "+getTitle()+"\n Author: "+getAuthor()+"\n Publisher: "+getPublisher()+"\n Publication Date: "+getPublishDate()+"\n Edition: "+getEdition()+"\n Number of Pages: "+getPages());
}
}
public void main(String[] args) {
Book b1 = new Book();
b1.setTitle("The Hobbit");
b1.setAuthor("J.R.R Tolkien");
b1.setPublisher("George Allen & Unwin");
b1.setPublishDate("21 September 1937");
b1.displayInfo();

System.out.println("==================================");

Encyclopedia b2 = new Encyclopedia();
b2.setTitle("The Illustrated Encyclopedia of the Universe");
b2.setAuthor("Ian Ridpath");
b2.setPublisher("Watson-Guptill");
b2.setPublishDate("2001");
b2.setEdition("2nd");
b2.setPages(384);
b2.displayInfo();

}
```
I didn't run into any challenges for this assignment.
