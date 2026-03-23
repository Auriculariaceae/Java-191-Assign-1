### Version 1.0
``` java
import java.util.Scanner;


static class inventoryItem{
    private String name;
    private String companyName;
    private String expiration;
    private String ageGroup;
   //gets are for displays now make sets underneath them

    public String getName(){
    return name;
    }
    public void setName(String name){
        this.name = name;
    }
    public String getCompanyName(){
        return companyName;
    }
    public void setCompanyName(String companyName){
        this.companyName = companyName;
    }
    public String getExpiration(){  //01-21-26 as an example or Jan 21st, 2026
        return expiration;
    }
    public void setExpiration(String expiration){
        this.expiration = expiration;
    }
    public String getAgeGroup(){  //18-21  21-30 as example input
        return ageGroup;
    }
    public void setAgeGroup(String ageGroup){
        this.ageGroup = ageGroup;
    }
    public void displayInfo(){
        System.out.println("Item name: "+getName()+", Company name: "+getCompanyName()+", Expiration: "+getExpiration()+", Age Group: "+getAgeGroup());
    }
}

class Painkillers extends inventoryItem {
    private String drugCompanyName;

    public String getDrugCompanyName() {
        return drugCompanyName;
    }
    public void setDrugCompanyName(String drugCompanyName){
        this.drugCompanyName = drugCompanyName;
    }
@Override
public void displayInfo(){
    System.out.println("Item name: "+getName()+", Drug company name: "+getDrugCompanyName()+", Expiration: "+getExpiration()+", Age Group: "+getAgeGroup());
}
}

class Bandages extends inventoryItem {
    private boolean waterproof;

    public boolean getWaterproof() {
        return waterproof;
    }
    public void setWaterproof(boolean waterproof){
        this.waterproof = waterproof;
    }
    @Override
    public void displayInfo(){
        System.out.println("Item name: "+getName()+", Company name: "+getCompanyName()+", Expiration: "+getExpiration()+", Age Group: "+getAgeGroup()+", Waterproof: "+getWaterproof());
    }
}


class Equipment extends inventoryItem {
    private double itemWeight;

    public double getItemWeight() {
        return itemWeight;
    }
    public void setItemWeight(double itemWeight){
        this.itemWeight = itemWeight;
    }
    @Override
    public void displayInfo(){
        System.out.println("Item name: "+getName()+", Company name: "+getCompanyName()+", Item Weight: "+getItemWeight());
    }
}
public static void main(String[] args) {
```
### Version 2 (exceptions)
```java
import java.util.Scanner;


static class inventoryItem{
    private String name;
    private String companyName;
    private String expiration;
    private String ageGroup;
   //gets are for displays now make sets underneath them

    public String getName(){
    return name;
    }
    public void setName(String name){
        this.name = name;
    }
    public String getCompanyName(){
        return companyName;
    }
    public void setCompanyName(String companyName){
        this.companyName = companyName;
    }
    public String getExpiration(){  //01-21-26 as an example or Jan 21st, 2026
        return expiration;
    }
    public void setExpiration(String expiration){
        this.expiration = expiration;
    }
    public String getAgeGroup(){  //18-21  21-30 as example input
        return ageGroup;
    }
    public void setAgeGroup(String ageGroup){
        this.ageGroup = ageGroup;
    }
    public void displayInfo(){
        System.out.println("Item name: "+getName()+", Company name: "+getCompanyName()+", Expiration: "+getExpiration()+", Age Group: "+getAgeGroup());
    }



    }

static class Painkillers extends inventoryItem {
    private String drugCompanyName;

    public String getDrugCompanyName() {
        return drugCompanyName;
    }
    public void setDrugCompanyName(String drugCompanyName){
        this.drugCompanyName = drugCompanyName;
    }
@Override
public void displayInfo(){
    System.out.println("Item name: "+getName()+", Drug company name: "+getDrugCompanyName()+", Expiration: "+getExpiration()+", Age Group: "+getAgeGroup());
}
}

static class Bandages extends inventoryItem {
    private String waterproof;

    public String getWaterproof() {
        return waterproof;
    }
    public void setWaterproof(String waterproof){
        this.waterproof = waterproof;
    }
    @Override
    public void displayInfo(){
        System.out.println("Item name: "+getName()+", Company name: "+getCompanyName()+", Expiration: "+getExpiration()+", Age Group: "+getAgeGroup()+", Waterproof: "+getWaterproof());
    }
}


static class Equipment extends inventoryItem {
    private double itemWeight;

    public double getItemWeight() {
        return itemWeight;
    }
    public void setItemWeight(double itemWeight){
        this.itemWeight = itemWeight;
    }
    @Override
    public void displayInfo(){
        System.out.println("Item name: "+getName()+", Company name: "+getCompanyName()+", Item Weight: "+getItemWeight()+"lbs");
    }
}
public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    System.out.println("What are you putting into inventory?");
    System.out.println("Press 1 for generic item, 2 for painkillers, 3 for bandages, or 4 for equipment.");
    try {
        String choice1 = sc.nextLine();
        int choice2 = Integer.parseInt(choice1);
        switch (choice2) {


            case 1:
                inventoryItem item1 = new inventoryItem();
                System.out.println("Product name");
                item1.setName(sc.nextLine());
                //sc.next();
                System.out.println("Product company");
                item1.setCompanyName(sc.nextLine());
                //sc.nextLine();
                System.out.println("Product expiration");
                item1.setExpiration(sc.nextLine());
                //sc.nextLine();
                System.out.println("Product age group");
                item1.setAgeGroup(sc.nextLine());
                //sc.nextLine();
                System.out.println("Product Information");
                item1.displayInfo();
                break;
            case 2:
                Painkillers pain1 = new Painkillers();
                System.out.println("Product name");
                pain1.setName(sc.nextLine());
                //sc.next();
                System.out.println("Product Drug company");
                pain1.setDrugCompanyName(sc.nextLine());
               //sc.nextLine();
                System.out.println("Product expiration");
                pain1.setExpiration(sc.nextLine());
                //sc.nextLine();
                System.out.println("Product age group");
                pain1.setAgeGroup(sc.nextLine());
                //sc.nextLine();
                System.out.println("Product Information");
                pain1.displayInfo();
                break;
            case 3:
                Bandages band1 = new Bandages();
                System.out.println("Product name");
                band1.setName(sc.nextLine());
                //sc.next();
                System.out.println("Product company");
                band1.setCompanyName(sc.nextLine());
               //sc.nextLine();
                System.out.println("Product expiration");
                band1.setExpiration(sc.nextLine());
                //sc.nextLine();
                System.out.println("Product age group");
                band1.setAgeGroup(sc.nextLine());
                //sc.nextLine();
                System.out.println("Is product waterproof?");
                band1.setWaterproof(sc.nextLine());

                System.out.println("Product Information");

                band1.displayInfo();
                break;
            case 4:
                Equipment equip = new Equipment();
                System.out.println("Product name");
                equip.setName(sc.nextLine());
                //sc.next();
                System.out.println("Product company");
                equip.setCompanyName(sc.nextLine());
                //sc.nextLine();
                try {
                    System.out.println("Product Weight (lbs)");
                    equip.setItemWeight(sc.nextDouble());
                } catch (InputMismatchException e){
                    System.out.println("Please input a valid number");
                    return;
                }
                System.out.println("Product Information");

                equip.displayInfo();
                break;
        }
    } catch (InputMismatchException e1){
        System.out.println("Please input a number 1-4");
    }
    }

```
### Version 3 (Custom Derived Exception)
```java
import java.util.Scanner;
public static class InvalidNegativeInputException extends Exception {
    public InvalidNegativeInputException() {
        super("Input is negative");
    }
}
static class inventoryItem{
    private String name;
    private String companyName;
    private String expiration;
    private String ageGroup;
   //gets are for displays now make sets underneath them

    public String getName(){
    return name;
    }
    public void setName(String name){
        this.name = name;
    }
    public String getCompanyName(){
        return companyName;
    }
    public void setCompanyName(String companyName){
        this.companyName = companyName;
    }
    public String getExpiration(){  //01-21-26 as an example or Jan 21st, 2026
        return expiration;
    }
    public void setExpiration(String expiration){
        this.expiration = expiration;
    }
    public String getAgeGroup(){  //18-21  21-30 as example input
        return ageGroup;
    }
    public void setAgeGroup(String ageGroup){
        this.ageGroup = ageGroup;
    }
    public void displayInfo(){
        System.out.println("Item name: "+getName()+", Company name: "+getCompanyName()+", Expiration: "+getExpiration()+", Age Group: "+getAgeGroup());
    }
    public static double getPositiveValue(Scanner sc)
            throws InvalidNegativeInputException {
        double inputVal = sc.nextDouble();
        if (inputVal < 0.0) {
            throw new InvalidNegativeInputException();
        }
        return inputVal;
    }


    }

static class Painkillers extends inventoryItem {
    private String drugCompanyName;

    public String getDrugCompanyName() {
        return drugCompanyName;
    }
    public void setDrugCompanyName(String drugCompanyName){
        this.drugCompanyName = drugCompanyName;
    }
@Override
public void displayInfo(){
    System.out.println("Item name: "+getName()+", Drug company name: "+getDrugCompanyName()+", Expiration: "+getExpiration()+", Age Group: "+getAgeGroup());
}
}

static class Bandages extends inventoryItem {
    private String waterproof;

    public String getWaterproof() {
        return waterproof;
    }
    public void setWaterproof(String waterproof){
        this.waterproof = waterproof;
    }
    @Override
    public void displayInfo(){
        System.out.println("Item name: "+getName()+", Company name: "+getCompanyName()+", Expiration: "+getExpiration()+", Age Group: "+getAgeGroup()+", Waterproof: "+getWaterproof());
    }
}


static class Equipment extends inventoryItem {
    private double itemWeight;

    public double getItemWeight() {
        return itemWeight;
    }
    public void setItemWeight(double itemWeight){
        this.itemWeight = itemWeight;
    }
    @Override
    public void displayInfo(){
        System.out.println("Item name: "+getName()+", Company name: "+getCompanyName()+", Item Weight: "+getItemWeight()+"lbs");
    }

}

public static void main(String[] args) {
 LinkedList<String> generic = new LinkedList<>();
 LinkedList<String> painkillers = new LinkedList<>();
 LinkedList<String> bandages = new LinkedList<>();
 LinkedList<String> equipment = new LinkedList<>();

    Scanner sc = new Scanner(System.in);
    System.out.println("What are you putting into inventory?");
    System.out.println("Press 1 for generic item, 2 for painkillers, 3 for bandages, or 4 for equipment.");

        try {
            String choice1 = sc.nextLine();
            int choice2 = Integer.parseInt(choice1);
            switch (choice2) {


                case 1:
                    inventoryItem item1 = new inventoryItem();
                    System.out.println("Product name");
                    item1.setName(sc.nextLine());

                    System.out.println("Product company");
                    item1.setCompanyName(sc.nextLine());

                    System.out.println("Product expiration");
                    item1.setExpiration(sc.nextLine());

                    System.out.println("Product age group");
                    item1.setAgeGroup(sc.nextLine());

                    System.out.println("Product Information");
                    item1.displayInfo();
                    generic.add(String.valueOf(item1));
                    //System.out.println(generic.getFirst());
                    break;
                case 2:
                    Painkillers pain1 = new Painkillers();
                    System.out.println("Product name");
                    pain1.setName(sc.nextLine());

                    System.out.println("Product Drug company");
                    pain1.setDrugCompanyName(sc.nextLine());

                    System.out.println("Product expiration");
                    pain1.setExpiration(sc.nextLine());

                    System.out.println("Product age group");
                    pain1.setAgeGroup(sc.nextLine());

                    System.out.println("Product Information");
                    pain1.displayInfo();
                    painkillers.add(String.valueOf(pain1));
                    break;
                case 3:
                    Bandages band1 = new Bandages();
                    System.out.println("Product name");
                    band1.setName(sc.nextLine());

                    System.out.println("Product company");
                    band1.setCompanyName(sc.nextLine());

                    System.out.println("Product expiration");
                    band1.setExpiration(sc.nextLine());

                    System.out.println("Product age group");
                    band1.setAgeGroup(sc.nextLine());

                    System.out.println("Is product waterproof?");
                    band1.setWaterproof(sc.nextLine());

                    System.out.println("Product Information");
                    bandages.add(String.valueOf(band1));
                    band1.displayInfo();
                    break;
                case 4:
                    Equipment equip = new Equipment();
                    System.out.println("Product name");
                    equip.setName(sc.nextLine());

                    System.out.println("Product company");
                    equip.setCompanyName(sc.nextLine());

                    try {
                        System.out.println("Product Weight (lbs)");
                        double itemWeight1= inventoryItem.getPositiveValue(sc);
                        if (itemWeight1<0){
                            throw new InvalidNegativeInputException();
                        }
                        equip.setItemWeight(itemWeight1);

                    } catch (Exception e) {
                        throw new InputMismatchException();
                    }
                    System.out.println("Product Information");
                    equipment.add(String.valueOf(equip));
                    equip.displayInfo();
                    break;
            }
        } catch (InputMismatchException e1) {
            System.out.println("Please input a number 1-4");
        }
    }

```
### I have absolutely no idea how to do exercise 3 correctly. I tried to decipher the previous labs related to it, but was unable to.
