# Design-Patterns

# FactoryPatternDemo

package Patterns;

interface Shape {
	   void draw();
	}
	class Rectangle implements Shape {

	   public void draw() {
	      System.out.println("Inside Rectangle::draw() method.");
	   }
	}
	class Square implements Shape {

	   public void draw() {
	      System.out.println("Inside Square::draw() method.");
	   }
	}
	 class Circle implements Shape {

	   public void draw() {
	      System.out.println("Inside Circle::draw() method.");
	   }
	}
	 class ShapeFactory { 
	   public Shape getShape(String shapeType){
	      if(shapeType == null){
	         return null;
	      }		
	      if(shapeType.equalsIgnoreCase("CIRCLE")){
	         return new Circle();
	         
	      } else if(shapeType.equalsIgnoreCase("RECTANGLE")){
	         return new Rectangle();
	         
	      } else if(shapeType.equalsIgnoreCase("SQUARE")){
	         return new Square();
	      }
	      
	      return null;
	   }
	}

	public class FactoryPatternDemo {

	   public static void main(String[] args) {
	      ShapeFactory shapeFactory = new ShapeFactory();

	      Shape shape1 = shapeFactory.getShape("CIRCLE");

	      shape1.draw();

	      Shape shape2 = shapeFactory.getShape("RECTANGLE");

	      shape2.draw();

	      Shape shape3 = shapeFactory.getShape("SQUARE");

	      shape3.draw();
	   }
	}
  
  
  
 #StatePatternDemo
 
  package Patterns;

interface State {
	   public void doAction(Context context);
	}

	class StartState implements State {

	   public void doAction(Context context) {
	      System.out.println("Player is in start state");
	      context.setState(this);	
	   }

	   public String toString(){
	      return "Start State";
	   }
	}

	class StopState implements State {

	   public void doAction(Context context) {
	      System.out.println("Player is in stop state");
	      context.setState(this);	
	   }

	   public String toString(){
	      return "Stop State";
	   }
	}

	class Context {
	   private State state;

	   public Context(){
	      state = null;
	   }

	   public void setState(State state){
	      this.state = state;		
	   }

	   public State getState(){
	      return state;
	   }
	}

	public class StatePatternDemo {
	   public static void main(String[] args) {
	      Context context = new Context();

	      StartState startState = new StartState();
	      startState.doAction(context);

	      System.out.println(context.getState().toString());

	      StopState stopState = new StopState();
	      stopState.doAction(context);

	      System.out.println(context.getState().toString());
	   }
	}

  
  
  
  
  
  
  
  
  
  #TemplatePatternDemo
  
  
  package Patterns;

abstract class Game {
	   abstract void initialize();
	   abstract void startPlay();
	   abstract void endPlay();

	   public final void play(){

	      initialize();

	      startPlay();

	      endPlay();
	   }
	}

	class Cricket extends Game {

	   void endPlay() {
	      System.out.println("Cricket Game Finished!");
	   }

	   void initialize() {
	      System.out.println("Cricket Game Initialized! Start playing.");
	   }

	   void startPlay() {
	      System.out.println("Cricket Game Started. Enjoy the game!");
	   }
	}

	class Football extends Game {

	   void endPlay() {
	      System.out.println("Football Game Finished!");
	   }

	   void initialize() {
	      System.out.println("Football Game Initialized! Start playing.");
	   }

	   void startPlay() {
	      System.out.println("Football Game Started. Enjoy the game!");
	   }
	}

	public class TemplatePatternDemo {
	   public static void main(String[] args) {

	      Game game = new Cricket();
	      game.play();
	      System.out.println();
	      game = new Football();
	      game.play();		
	   }
     
     
     
     
     
     
     
     
     
     
     
     
     
     
     
     
 #TemplatePatternDemo   
     
     package Patterns;

import java.util.ArrayList;
import java.util.List;

class Employee {
   private String name;
   private String dept;
   private int salary;
   private List<Employee> subordinates;

   // constructor
   public Employee(String name,String dept, int sal) {
      this.name = name;
      this.dept = dept;
      this.salary = sal;
      subordinates = new ArrayList<Employee>();
   }

   public void add(Employee e) {
      subordinates.add(e);
   }

   public void remove(Employee e) {
      subordinates.remove(e);
   }

   public List<Employee> getSubordinates(){
     return subordinates;
   }

   public String toString(){
      return ("Employee :[ Name : " + name + ", dept : " + dept + ", salary :" + salary+" ]");
   }   
}
public class CompositePatternDemo {
   public static void main(String[] args) {
   
      Employee CEO = new Employee("Johny","CEO", 30000);

      Employee headSales = new Employee("Robert","Head Sales", 20000);

      Employee headMarketing = new Employee("Michel","Head Marketing", 20000);

      Employee clerk1 = new Employee("Laura","Marketing", 10000);
      Employee clerk2 = new Employee("Bob","Marketing", 10000);

      Employee salesExecutive1 = new Employee("Richard","Sales", 10000);
      Employee salesExecutive2 = new Employee("Rob","Sales", 10000);

      CEO.add(headSales);
      CEO.add(headMarketing);

      headSales.add(salesExecutive1);
      headSales.add(salesExecutive2);

      headMarketing.add(clerk1);
      headMarketing.add(clerk2);

      //print all employees of the organization
      System.out.println(CEO); 
      
      for (Employee headEmployee : CEO.getSubordinates()) {
         System.out.println(headEmployee);
         
         for (Employee employee : headEmployee.getSubordinates()) {
            System.out.println(employee);
         }
      }		
   }
}











# AdapterPatternDemo

package Patterns;

interface MediaPlayer {
	   public void play(String audioType, String fileName);
	}

	interface AdvancedMediaPlayer {	
	   public void playVlc(String fileName);
	   public void playMp4(String fileName);
	}
	class VlcPlayer implements AdvancedMediaPlayer{
	 
	   public void playVlc(String fileName) {
	      System.out.println("Playing vlc file. Name: "+ fileName);		
	   }

	   public void playMp4(String fileName) {
	      
	   }
	}
	class Mp4Player implements AdvancedMediaPlayer{

	   public void playVlc(String fileName) {

	   }

	   public void playMp4(String fileName) {
	      System.out.println("Playing mp4 file. Name: "+ fileName);		
	   }
	}
	class MediaAdapter implements MediaPlayer {

	   AdvancedMediaPlayer advancedMusicPlayer;

	   public MediaAdapter(String audioType){
	   
	      if(audioType.equalsIgnoreCase("vlc") ){
	         advancedMusicPlayer = new VlcPlayer();			
	         
	      }else if (audioType.equalsIgnoreCase("mp4")){
	         advancedMusicPlayer = new Mp4Player();
	      }	
	   }

	   public void play(String audioType, String fileName) {
	   
	      if(audioType.equalsIgnoreCase("vlc")){
	         advancedMusicPlayer.playVlc(fileName);
	      }
	      else if(audioType.equalsIgnoreCase("mp4")){
	         advancedMusicPlayer.playMp4(fileName);
	      }
	   }
	}

	class AudioPlayer implements MediaPlayer {
	   MediaAdapter mediaAdapter; 

	   public void play(String audioType, String fileName) {		

	      if(audioType.equalsIgnoreCase("mp3")){
	         System.out.println("Playing mp3 file. Name: " + fileName);			
	      } 
	      
	      else if(audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")){
	         mediaAdapter = new MediaAdapter(audioType);
	         mediaAdapter.play(audioType, fileName);
	      }
	      
	      else{
	         System.out.println("Invalid media. " + audioType + " format not supported");
	      }
	   }   
	}
	public class AdapterPatternDemo {
	   public static void main(String[] args) {
	      AudioPlayer audioPlayer = new AudioPlayer();

	      audioPlayer.play("mp3", "beyond the horizon.mp3");
	      audioPlayer.play("mp4", "alone.mp4");
	      audioPlayer.play("vlc", "far far away.vlc");
	      audioPlayer.play("avi", "mind me.avi");
	   }
	}
  
  
  
  
  
  
#SingleObject  
  
  
  package Patterns;

class SingleObject {

	   //create an object of SingleObject
	   private static SingleObject instance = new SingleObject();

	   //make the constructor private so that this class cannot be
	   //instantiated
	   private SingleObject(){}

	   //Get the only object available
	   public static SingleObject getInstance(){
	      return instance;
	   }

	   public void showMessage(){
	      System.out.println("Hello World!");
	   }
	}

	public class SingletonPatternDemo {
	   public static void main(String[] args) {

	      //illegal construct
	      //Compile Time Error: The constructor SingleObject() is not visible
	      //SingleObject object = new SingleObject();

	      //Get the only object available
	      SingleObject object = SingleObject.getInstance();

	      //show the message
	      object.showMessage();
	   }
	}
