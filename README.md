import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyEvent;
public class BuildingEstimationGUI extends JFrame {

    // Define cost constants per square meter and per floor
    static final double COST_EXCAVATION = 50; // cost per square meter
    static final double COST_FOUNDATION = 100; // cost per square meter
    static final double COST_STRUCTURE = 500; // cost per square meter per floor
    static final double COST_WALLS = 300; // cost per square meter per floor
    static final double COST_ROOF = 200; // cost per square meter
    static final double COST_FLOORING = 100; // cost per square meter per floor
    static final double COST_PAINTING = 50; // cost per square meter per floor

    private JTextField areaField;
    private JTextField floorsField;
    private JTextArea resultArea;

    public BuildingEstimationGUI() {
        setTitle("Building Estimation and Costing Tool");
        setSize(400, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        setLayout(null);

        JLabel areaLabel = new JLabel("Total Area (sq meters):");
        areaLabel.setBounds(20, 20, 150, 30);
        add(areaLabel);

        areaField = new JTextField();
        areaField.setBounds(180, 20, 150, 30);
        add(areaField);

        JLabel floorsLabel = new JLabel("Number of Floors:");
        floorsLabel.setBounds(20, 60, 150, 30);
        add(floorsLabel);

        floorsField = new JTextField();
        floorsField.setBounds(180, 60, 150, 30);
        add(floorsField);

        JButton calculateButton = new JButton("Calculate");
        calculateButton.setBounds(20, 100, 310, 30);
        add(calculateButton);

        resultArea = new JTextArea();
        resultArea.setBounds(20, 140, 310, 200);
        resultArea.setEditable(false);
        add(resultArea);

        calculateButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                calculateCosts();
            }
        });
    }

    private void calculateCosts() {
        try {
            double area = Double.parseDouble(areaField.getText());
            int floors = Integer.parseInt(floorsField.getText());

            // Calculate costs
            double costExcavation = area * COST_EXCAVATION;
            double costFoundation = area * COST_FOUNDATION;
            double costStructure = area * floors * COST_STRUCTURE;
            double costWalls = area * floors * COST_WALLS;
            double costRoof = area * COST_ROOF;
            double costFlooring = area * floors * COST_FLOORING;
            double costPainting = area * floors * COST_PAINTING;

            // Calculate total cost
            double totalCost = costExcavation + costFoundation + costStructure + costWalls + costRoof + costFlooring + costPainting;

            // Display the costs
            resultArea.setText(String.format(
                "Cost Estimation:\n" +
                "Excavation: $%.2f\n" +
                "Foundation: $%.2f\n" +
                "Structure: $%.2f\n" +
                "Walls: $%.2f\n" +
                "Roof: $%.2f\n" +
                "Flooring: $%.2f\n" +
                "Painting: $%.2f\n" +
                "---------------------------\n" +
                "Total Estimated Cost: $%.2f",
                costExcavation, costFoundation, costStructure, costWalls, costRoof, costFlooring, costPainting, totalCost
            ));

        } catch (NumberFormatException e) {
            JOptionPane.showMessageDialog(this, "Please enter valid numbers for area and floors.", "Input Error", JOptionPane.ERROR_MESSAGE);
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new BuildingEstimationGUI().setVisible(true);
            }
        });
    }
}
