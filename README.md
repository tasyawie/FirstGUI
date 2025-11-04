import javax.swing.*;
import javax.swing.filechooser.FileNameExtensionFilter;
import java.awt.*;
import java.awt.event.*;
import java.io.*;
import java.util.*;

public class CollegePortalGUI extends JFrame {
    private CardLayout cardLayout;
    private JPanel mainPanel;
    private Map<String, StudentAccount> accounts;
    private String selectedImagePath = null;
    
    // Colors matching the theme
    private final Color MAROON = new Color(128, 0, 0);
    private final Color LIGHT_GRAY = new Color(240, 240, 240);
    
    public CollegePortalGUI() {
        accounts = new HashMap<>();
        setTitle("CNSC - College of Computing and Multimedia Studies");
        setSize(1100, 700);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        
        cardLayout = new CardLayout();
        mainPanel = new JPanel(cardLayout);
        
        mainPanel.add(createMainMenuPanel(), "MAIN");
        mainPanel.add(createRegistrationPanel(), "REGISTRATION");
        mainPanel.add(createConfirmationPanel(), "CONFIRMATION");
        mainPanel.add(createLoginPanel(), "LOGIN");
        mainPanel.add(createSignUpPanel(), "SIGNUP");
        
        add(mainPanel);
        setVisible(true);
    }
    
    private JPanel createMainMenuPanel() {
        JPanel panel = new JPanel(null);
        panel.setBackground(LIGHT_GRAY);
        
        // Background image placeholder
        JLabel bgLabel = new JLabel();
        bgLabel.setBounds(0, 0, 1100, 700);
        
        // Logo (top left)
        JLabel logoLabel = new JLabel("CNSU");
        logoLabel.setBounds(30, 20, 80, 80);
        logoLabel.setOpaque(true);
        logoLabel.setBackground(MAROON);
        logoLabel.setForeground(Color.WHITE);
        logoLabel.setHorizontalAlignment(SwingConstants.CENTER);
        logoLabel.setFont(new Font("Arial", Font.BOLD, 16));
        
        // Title
        JLabel titleLabel = new JLabel("College of Computing and Multimedia Studies");
        titleLabel.setBounds(120, 35, 600, 40);
        titleLabel.setFont(new Font("Arial", Font.BOLD, 24));
        titleLabel.setForeground(Color.WHITE);
        
        // Admin Button
        JButton adminBtn = createStyledButton("Admin");
        adminBtn.setBounds(400, 280, 300, 60);
        adminBtn.addActionListener(e -> {
            JOptionPane.showMessageDialog(this, "Admin panel not implemented in this demo");
        });
        
        // Student Assistant Button
        JButton studentBtn = createStyledButton("Student Assistant");
        studentBtn.setBounds(400, 370, 300, 60);
        studentBtn.addActionListener(e -> {
            selectedImagePath = null;
            cardLayout.show(mainPanel, "REGISTRATION");
        });
        
        // University Logo (bottom right)
        JLabel uniLogo = new JLabel();
        uniLogo.setBounds(900, 450, 150, 150);
        uniLogo.setOpaque(true);
        uniLogo.setBackground(Color.WHITE);
        uniLogo.setBorder(BorderFactory.createLineBorder(MAROON, 3));
        
        JLabel uniText = new JLabel("<html><center>CAMARINES<br>NORTE STATE<br>UNIVERSITY<br>1992</center></html>");
        uniText.setHorizontalAlignment(SwingConstants.CENTER);
        uniText.setFont(new Font("Arial", Font.BOLD, 12));
        uniLogo.setLayout(new BorderLayout());
        uniLogo.add(uniText, BorderLayout.CENTER);
        
        // Maroon wave decoration
        JPanel wavePanel = new JPanel();
        wavePanel.setBounds(0, 500, 1100, 200);
        wavePanel.setBackground(MAROON);
        
        panel.add(logoLabel);
        panel.add(titleLabel);
        panel.add(adminBtn);
        panel.add(studentBtn);
        panel.add(uniLogo);
        panel.add(wavePanel);
        
        return panel;
    }
    
    private JPanel createRegistrationPanel() {
        JPanel panel = new JPanel(null);
        panel.setBackground(LIGHT_GRAY);
        
        // Picture upload area
        JPanel picturePanel = new JPanel();
        picturePanel.setBounds(100, 110, 190, 185);
        picturePanel.setBackground(Color.WHITE);
        picturePanel.setBorder(BorderFactory.createLineBorder(Color.BLACK, 2));
        picturePanel.setLayout(new BorderLayout());
        
        JLabel pictureLabel = new JLabel("<html><center>1×1 Picture<br><br>Click to Upload</center></html>");
        pictureLabel.setHorizontalAlignment(SwingConstants.CENTER);
        pictureLabel.setFont(new Font("Arial", Font.ITALIC, 16));
        picturePanel.add(pictureLabel, BorderLayout.CENTER);
        
        picturePanel.addMouseListener(new MouseAdapter() {
            public void mouseClicked(MouseEvent e) {
                JFileChooser fileChooser = new JFileChooser();
                fileChooser.setFileFilter(new FileNameExtensionFilter("Image files", "jpg", "jpeg", "png"));
                int result = fileChooser.showOpenDialog(panel);
                if (result == JFileChooser.APPROVE_OPTION) {
                    selectedImagePath = fileChooser.getSelectedFile().getAbsolutePath();
                    pictureLabel.setText("<html><center>Image Selected<br>" + 
                        fileChooser.getSelectedFile().getName() + "</center></html>");
                }
            }
        });
        
        // Form fields
        int fieldX = 370;
        int fieldWidth = 590;
        int fieldHeight = 40;
        
        JLabel nameLabel = new JLabel("Enter Your Name");
        nameLabel.setBounds(fieldX, 100, 300, 30);
        nameLabel.setFont(new Font("Arial", Font.PLAIN, 18));
        
        JTextField nameField = new JTextField();
        nameField.setBounds(fieldX, 130, fieldWidth, fieldHeight);
        nameField.setFont(new Font("Arial", Font.PLAIN, 16));
        
        JLabel courseLabel = new JLabel("Course & Year & Section");
        courseLabel.setBounds(fieldX, 190, 300, 30);
        courseLabel.setFont(new Font("Arial", Font.PLAIN, 18));
        
        JTextField courseField = new JTextField();
        courseField.setBounds(fieldX, 220, fieldWidth, fieldHeight);
        courseField.setFont(new Font("Arial", Font.PLAIN, 16));
        
        JLabel phoneLabel = new JLabel("Cellphone Number");
        phoneLabel.setBounds(fieldX, 280, 300, 30);
        phoneLabel.setFont(new Font("Arial", Font.PLAIN, 18));
        
        JTextField phoneField = new JTextField();
        phoneField.setBounds(fieldX, 310, fieldWidth, fieldHeight);
        phoneField.setFont(new Font("Arial", Font.PLAIN, 16));
        
        JLabel emailLabel = new JLabel("Email");
        emailLabel.setBounds(fieldX, 370, 300, 30);
        emailLabel.setFont(new Font("Arial", Font.PLAIN, 18));
        
        JTextField emailField = new JTextField();
        emailField.setBounds(fieldX, 400, fieldWidth, fieldHeight);
        emailField.setFont(new Font("Arial", Font.PLAIN, 16));
        
        // Turn In button
        JButton turnInBtn = createStyledButton("Turn In");
        turnInBtn.setBounds(930, 37, 130, 50);
        turnInBtn.addActionListener(e -> {
            if (nameField.getText().trim().isEmpty() || 
                courseField.getText().trim().isEmpty() ||
                phoneField.getText().trim().isEmpty() ||
                emailField.getText().trim().isEmpty() ||
                selectedImagePath == null) {
                JOptionPane.showMessageDialog(this, "Please fill in all fields and upload a picture!");
            } else {
                // Store pending registration
                String studentId = "SA" + System.currentTimeMillis();
                StudentAccount account = new StudentAccount(
                    nameField.getText().trim(),
                    studentId,
                    courseField.getText().trim(),
                    false // Not approved yet
                );
                accounts.put(studentId, account);
                
                // Clear fields
                nameField.setText("");
                courseField.setText("");
                phoneField.setText("");
                emailField.setText("");
                selectedImagePath = null;
                pictureLabel.setText("<html><center>1×1 Picture<br><br>Click to Upload</center></html>");
                
                cardLayout.show(mainPanel, "CONFIRMATION");
            }
        });
        
        // Maroon wave at bottom
        JPanel wavePanel = new JPanel();
        wavePanel.setBounds(0, 500, 1100, 200);
        wavePanel.setBackground(MAROON);
        
        panel.add(picturePanel);
        panel.add(nameLabel);
        panel.add(nameField);
        panel.add(courseLabel);
        panel.add(courseField);
        panel.add(phoneLabel);
        panel.add(phoneField);
        panel.add(emailLabel);
        panel.add(emailField);
        panel.add(turnInBtn);
        panel.add(wavePanel);
        
        return panel;
    }
    
    private JPanel createConfirmationPanel() {
        JPanel panel = new JPanel(null);
        panel.setBackground(Color.WHITE);
        
        // Check icon
        JLabel checkIcon = new JLabel("✓");
        checkIcon.setBounds(450, 150, 200, 200);
        checkIcon.setFont(new Font("Arial", Font.BOLD, 150));
        checkIcon.setForeground(new Color(100, 180, 0));
        checkIcon.setHorizontalAlignment(SwingConstants.CENTER);
        
        JLabel messageLabel = new JLabel("Request Sent!");
        messageLabel.setBounds(350, 350, 400, 50);
        messageLabel.setFont(new Font("Arial", Font.BOLD, 36));
        messageLabel.setHorizontalAlignment(SwingConstants.CENTER);
        
        JButton returnBtn = createStyledButton("Return");
        returnBtn.setBounds(450, 430, 200, 60);
        returnBtn.addActionListener(e -> cardLayout.show(mainPanel, "MAIN"));
        
        panel.add(checkIcon);
        panel.add(messageLabel);
        panel.add(returnBtn);
        
        return panel;
    }
    
    private JPanel createLoginPanel() {
        JPanel panel = new JPanel(null);
        panel.setBackground(LIGHT_GRAY);
        
        // Logos
        JLabel logo1 = new JLabel("CNSU");
        logo1.setBounds(40, 30, 60, 60);
        logo1.setOpaque(true);
        logo1.setBackground(MAROON);
        logo1.setForeground(Color.WHITE);
        logo1.setHorizontalAlignment(SwingConstants.CENTER);
        
        JLabel logo2 = new JLabel("▲");
        logo2.setBounds(120, 30, 60, 60);
        logo2.setOpaque(true);
        logo2.setBackground(MAROON);
        logo2.setForeground(Color.YELLOW);
        logo2.setHorizontalAlignment(SwingConstants.CENTER);
        logo2.setFont(new Font("Arial", Font.BOLD, 30));
        
        // Title
        JLabel titleLabel = new JLabel("Log in");
        titleLabel.setBounds(320, 80, 450, 80);
        titleLabel.setFont(new Font("Arial", Font.BOLD, 72));
        titleLabel.setHorizontalAlignment(SwingConstants.CENTER);
        
        JLabel welcomeLabel = new JLabel("Welcome! Please log in your account.");
        welcomeLabel.setBounds(320, 160, 450, 30);
        welcomeLabel.setFont(new Font("Arial", Font.PLAIN, 18));
        welcomeLabel.setHorizontalAlignment(SwingConstants.CENTER);
        
        // Student ID
        JLabel idLabel = new JLabel("Student ID");
        idLabel.setBounds(315, 230, 200, 30);
        idLabel.setFont(new Font("Arial", Font.PLAIN, 18));
        
        JTextField idField = new JTextField();
        idField.setBounds(315, 265, 460, 45);
        idField.setFont(new Font("Arial", Font.PLAIN, 16));
        
        // Password
        JLabel passLabel = new JLabel("Password");
        passLabel.setBounds(315, 340, 200, 30);
        passLabel.setFont(new Font("Arial", Font.PLAIN, 18));
        
        JPasswordField passField = new JPasswordField();
        passField.setBounds(315, 375, 460, 45);
        passField.setFont(new Font("Arial", Font.PLAIN, 16));
        
        // Sign up link
        JLabel signupLabel = new JLabel("<html>Don't have an account? <font color='maroon'>Sign up</font></html>");
        signupLabel.setBounds(315, 440, 300, 30);
        signupLabel.setFont(new Font("Arial", Font.ITALIC, 14));
        signupLabel.setCursor(new Cursor(Cursor.HAND_CURSOR));
        signupLabel.addMouseListener(new MouseAdapter() {
            public void mouseClicked(MouseEvent e) {
                cardLayout.show(mainPanel, "SIGNUP");
            }
        });
        
        // Log in button
        JButton loginBtn = createStyledButton("Log in");
        loginBtn.setBounds(445, 495, 200, 50);
        loginBtn.addActionListener(e -> {
            String id = idField.getText().trim();
            String pass = new String(passField.getPassword());
            
            if (accounts.containsKey(id)) {
                StudentAccount account = accounts.get(id);
                if (account.isApproved() && account.getPassword().equals(pass)) {
                    JOptionPane.showMessageDialog(this, "Login successful!\nWelcome, " + account.getName());
                    idField.setText("");
                    passField.setText("");
                } else if (!account.isApproved()) {
                    JOptionPane.showMessageDialog(this, "Your account is pending admin approval.");
                } else {
                    JOptionPane.showMessageDialog(this, "Incorrect password!");
                }
            } else {
                JOptionPane.showMessageDialog(this, "Student ID not found!");
            }
        });
        
        // Maroon wave
        JPanel wavePanel = new JPanel();
        wavePanel.setBounds(800, 0, 300, 700);
        wavePanel.setBackground(MAROON);
        
        panel.add(logo1);
        panel.add(logo2);
        panel.add(titleLabel);
        panel.add(welcomeLabel);
        panel.add(idLabel);
        panel.add(idField);
        panel.add(passLabel);
        panel.add(passField);
        panel.add(signupLabel);
        panel.add(loginBtn);
        panel.add(wavePanel);
        
        return panel;
    }
    
    private JPanel createSignUpPanel() {
        JPanel panel = new JPanel(null);
        panel.setBackground(LIGHT_GRAY);
        
        // Title
        JLabel titleLabel = new JLabel("Sign up");
        titleLabel.setBounds(150, 50, 400, 60);
        titleLabel.setFont(new Font("Arial", Font.BOLD | Font.ITALIC, 56));
        
        JLabel welcomeLabel = new JLabel("Welcome! Please create an account.");
        welcomeLabel.setBounds(150, 115, 400, 30);
        welcomeLabel.setFont(new Font("Arial", Font.PLAIN, 16));
        
        int fieldX = 150;
        int fieldWidth = 510;
        
        // Name
        JLabel nameLabel = new JLabel("Name");
        nameLabel.setBounds(fieldX, 170, 200, 25);
        nameLabel.setFont(new Font("Arial", Font.PLAIN, 16));
        
        JTextField nameField = new JTextField();
        nameField.setBounds(fieldX, 200, fieldWidth, 40);
        
        // ID Number
        JLabel idLabel = new JLabel("ID Number");
        idLabel.setBounds(fieldX, 250, 200, 25);
        idLabel.setFont(new Font("Arial", Font.PLAIN, 16));
        
        JTextField idField = new JTextField();
        idField.setBounds(fieldX, 280, fieldWidth, 40);
        
        // Department
        JLabel deptLabel = new JLabel("Department / Office");
        deptLabel.setBounds(fieldX, 330, 200, 25);
        deptLabel.setFont(new Font("Arial", Font.PLAIN, 16));
        
        JTextField deptField = new JTextField();
        deptField.setBounds(fieldX, 360, fieldWidth, 40);
        
        // Password
        JLabel passLabel = new JLabel("Password");
        passLabel.setBounds(fieldX, 410, 200, 25);
        passLabel.setFont(new Font("Arial", Font.PLAIN, 16));
        
        JPasswordField passField = new JPasswordField();
        passField.setBounds(fieldX, 440, fieldWidth, 40);
        
        // Login link
        JLabel loginLabel = new JLabel("<html>Already have an account? <font color='maroon'>Log in</font></html>");
        loginLabel.setBounds(fieldX, 490, 300, 30);
        loginLabel.setFont(new Font("Arial", Font.ITALIC, 14));
        loginLabel.setCursor(new Cursor(Cursor.HAND_CURSOR));
        loginLabel.addMouseListener(new MouseAdapter() {
            public void mouseClicked(MouseEvent e) {
                cardLayout.show(mainPanel, "LOGIN");
            }
        });
        
        // Sign up button
        JButton signupBtn = createStyledButton("Sign up");
        signupBtn.setBounds(300, 535, 210, 50);
        signupBtn.addActionListener(e -> {
            String name = nameField.getText().trim();
            String id = idField.getText().trim();
            String dept = deptField.getText().trim();
            String pass = new String(passField.getPassword());
            
            if (name.isEmpty() || id.isEmpty() || dept.isEmpty() || pass.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Please fill in all fields!");
            } else if (accounts.containsKey(id)) {
                JOptionPane.showMessageDialog(this, "This ID already exists!");
            } else {
                StudentAccount account = new StudentAccount(name, id, dept, true);
                account.setPassword(pass);
                accounts.put(id, account);
                
                JOptionPane.showMessageDialog(this, "Account created successfully!\nYou can now log in.");
                
                nameField.setText("");
                idField.setText("");
                deptField.setText("");
                passField.setText("");
                
                cardLayout.show(mainPanel, "LOGIN");
            }
        });
        
        // Maroon wave
        JPanel wavePanel = new JPanel();
        wavePanel.setBounds(750, 0, 350, 700);
        wavePanel.setBackground(MAROON);
        
        panel.add(titleLabel);
        panel.add(welcomeLabel);
        panel.add(nameLabel);
        panel.add(nameField);
        panel.add(idLabel);
        panel.add(idField);
        panel.add(deptLabel);
        panel.add(deptField);
        panel.add(passLabel);
        panel.add(passField);
        panel.add(loginLabel);
        panel.add(signupBtn);
        panel.add(wavePanel);
        
        return panel;
    }
    
    private JButton createStyledButton(String text) {
        JButton button = new JButton(text);
        button.setFont(new Font("Arial", Font.BOLD, 18));
        button.setBackground(MAROON);
        button.setForeground(Color.WHITE);
        button.setFocusPainted(false);
        button.setBorderPainted(false);
        button.setCursor(new Cursor(Cursor.HAND_CURSOR));
        
        button.addMouseListener(new MouseAdapter() {
            public void mouseEntered(MouseEvent e) {
                button.setBackground(new Color(150, 0, 0));
            }
            public void mouseExited(MouseEvent e) {
                button.setBackground(MAROON);
            }
        });
        
        return button;
    }
    
    // Inner class for student accounts
    private class StudentAccount {
        private String name;
        private String studentId;
        private String courseOrDept;
        private boolean approved;
        private String password;
        
        public StudentAccount(String name, String studentId, String courseOrDept, boolean approved) {
            this.name = name;
            this.studentId = studentId;
            this.courseOrDept = courseOrDept;
            this.approved = approved;
            this.password = "";
        }
        
        public String getName() { return name; }
        public String getStudentId() { return studentId; }
        public boolean isApproved() { return approved; }
        public void setApproved(boolean approved) { this.approved = approved; }
        public String getPassword() { return password; }
        public void setPassword(String password) { this.password = password; }
    }
    
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new CollegePortalGUI());
    }
}
