/**
 * Write a description of class RegularMember here.
 *The RegularMember class represents a gym member with a basic membership plan. It extends the 
 *GymMember class, inheriting common attributes and behaviors, while adding specific features
 *like plan, price, attendance tracking, and eligibility for plan upgrades.
 
  * @author (Renu Kumari Kapar)
  * @version (2025-03-06)
 */

 public class RegularMember extends GymMember {
    //Attributes
     private final int attendanceLimit; 
    private boolean isEligibleForUpgrade;
    private String removalReason;
    private String referralSource;
    private String plan;
    private double price;

    //Costructor
    public RegularMember(int id, String name, String location, String phone, String email, String gender, String DOB, String membershipStartDate, String referralSource) {
        super(id, name, location, phone, email, gender, DOB, membershipStartDate);
        this.referralSource = referralSource;
        this.isEligibleForUpgrade = false;
        this.plan = "Basic";
        this.price = 6500.0;
        this.removalReason = ""; 
        this.attendanceLimit =30;
    }
    
    //Getters methods
    public int getAttendanceLimit() {
        return attendanceLimit;
    }

    public boolean isEligibleForUpgrade() {
        return isEligibleForUpgrade;
    }

    public String getRemovalReason() {
        return removalReason;
    }

    public String getReferralSource() {
        return referralSource;
    }

    public String getPlan() {
        return plan;
    }

    public double getPrice() {
        return price;
    }

    
    // Abstract method markAttendance() from GymMember
    public void markAttendance() {
        attendance ++; 
        loyaltyPoints += 5; 
        if (getAttendance() >= attendanceLimit) {
            isEligibleForUpgrade = true; 
        }
    }

    // Method to get the price of a provided plan
    public double getPlanPrice(String plan) {
        switch (plan) {
            case "basic":
                return 6500.0;
            case "standard":
                return 12500.0;
            case "deluxe":
                return 18500.0;
            default:
                return -1.0; 
        }
    }

    // Method to upgrade the plan
    public String upgradePlan(String newPlan) {
        if (newPlan.equals(plan)) {
            return "You are already subscribed to the " + newPlan + " plan.";
        }
        
        if (!isEligibleForUpgrade) {
            return "You are not eligible for an upgrade.";
        }
        
        double newPrice = getPlanPrice(newPlan);
        if (newPrice == -1.0) {
            return "Invalid plan chosen.";
        }
        
        this.plan = newPlan;
        this.price = newPrice;
        isEligibleForUpgrade = false; 
        return "Your plan has been upgraded to " + newPlan + " with a price of " + newPrice;
    }

     // Method to revert RegularMember
    public void revertRegularMember(String removalReason) {
        super.resetMember(); 
        this.isEligibleForUpgrade = false;
        this.plan = "Basic";
        this.price = 6500.0;
        this.removalReason = removalReason; 
    }

    public void display() {
        super.display(); 
        System.out.println("Plan: " + this. plan);
        System.out.println("Price: " + this. price);
        if (!removalReason.isEmpty()) {
            System.out.println("Removal Reason: " + removalReason);
        }
    }
}
