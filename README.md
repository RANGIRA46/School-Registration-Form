dleNameField = new JTextField();
        JLaderComboBox = new JComboBox<>(genders);

        personalPanel.add(firstNameLabel);
        personalPanel.add(firstNameField);
        personalPanel.add(middleNameLabel);
        personalPanel.add(middleNameField);
        personalPanel.add(lastNameLabel);
        personalPanel.add(lastNameField);
        personalPanel.add(genderLabel);
        personalPanel.add(genderComboBox);

        JLabel dobLabel = new JLabel("Date of Birth:");
        yearComboBox = new JComboBox<>(getYearArray());
        monthComboBox = new JComboBox<>(getMonthArray());
        dayComboBox = new JComboBox<>(getDayArray(1));
        monthComboBox.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                int selectedMonth = (int) monthComboBox.getSelectedItem();
                int maxDay = getMaxDay(selectedMonth);
                dayComboBox.setModel(new DefaultComboBoxModel<>(getDayArray(maxDay)));
            }
        });

        personalPanel.add(dobLabel);
        personalPanel.add(yearComboBox);
        personalPanel.add(monthComboBox);
        personalPanel.add(dayComboBox);

        JLabel nidLabel = new JLabel("National ID Number:");
        nidField = new JTextField();
        personalPanel.add(nidLabel);
        personalPanel.add(nidField);

        JButton nextButton = new JButton("Next");
        nextButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                if (validatePersonalData() && validateDOB()) {
                    int age = calculateAge();
                    if (age > 16) {
                        if (nidField.getText().isEmpty()) {
                            JOptionPane.showMessageDialog(SchoolRegistrationForm.this, "Please provide National ID Number for students above 16.", "Error", JOptionPane.ERROR_MESSAGE);
                            return;
                        }
                    }
                    showBirthPlaceWindow();
                } else {
                    JOptionPane.showMessageDialog(SchoolRegistrationForm.this, "Please fill out all fields correctly.", "Error", JOptionPane.ERROR_MESSAGE);
                }
            }
        });
        personalPanel.add(nextButton);

        currentPanel = personalPanel;
        add(currentPanel);

        setVisible(true);
    }

    private boolean validatePersonalData() {
        String firstName = firstNameField.getText().trim();
        String lastName = lastNameField.getText().trim();
        return !firstName.isEmpty() && !lastName.isEmpty();
    }

    private boolean validateDOB() {
        int year = (int) yearComboBox.getSelectedItem();
        int month = (int) monthComboBox.getSelectedItem();
        int day = (int) dayComboBox.getSelectedItem();

        LocalDate birthDate = LocalDate.of(year, month, day);
        LocalDate currentDate = LocalDate.now();

        return birthDate.isBefore(currentDate);
    }

    private int calculateAge() {
        int year = (int) yearComboBox.getSelectedItem();
        int month = (int) monthComboBox.getSelectedItem();
        int day = (int) dayComboBox.getSelectedItem();

        LocalDate birthDate = LocalDate.of(year, month, day);
        LocalDate currentDate = LocalDate.now();

        return currentDate.getYear() - birthDate.getYear();
    }

    private void showBirthPlaceWindow() {
        getContentPane().removeAll();
        revalidate();
        repaint();

        // Second window: Birth Place
        JPanel birthPlacePanel = new JPanel(new GridLayout(7, 2, 10, 10));
        JLabel countryLabel = new JLabel("Country:");
        birthCountryField = new JTextField();
        JLabel provinceLabel = new JLabel("Province:");
        birthProvinceField = new JTextField();
        JLabel districtLabel = new JLabel("District:");
        birthDistrictField = new JTextField();
        JLabel sectorLabel = new JLabel("Sector:");
        birthSectorField = new JTextField();
        JLabel cellLabel = new JLabel("Cell:");
        birthCellField = new JTextField();
        JLabel villageLabel = new JLabel("Village:");
        birthVillageField = new JTextField();

        birthPlacePanel.add(countryLabel);
        birthPlacePanel.add(birthCountryField);
        birthPlacePanel.add(provinceLabel);
        birthPlacePanel.add(birthProvinceField);
        birthPlacePanel.add(districtLabel);
        birthPlacePanel.add(birthDistrictField);
        birthPlacePanel.add(sectorLabel);
        birthPlacePanel.add(birthSectorField);
        birthPlacePanel.add(cellLabel);
        birthPlacePanel.add(birthCellField);
        birthPlacePanel.add(villageLabel);
        birthPlacePanel.add(birthVillageField);

        JButton nextButton = new JButton("Next");
        nextButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                showCurrentLocationWindow();
            }
        });
        birthPlacePanel.add(nextButton);

        currentPanel = birthPlacePanel;
        add(currentPanel);

        revalidate();
    }

    private void showCurrentLocationWindow() {
        getContentPane().removeAll();
        revalidate();
        repaint();

        // Third window: Current Location
        JPanel currentLocationPanel = new JPanel(new GridLayout(7, 2, 10, 10));
        JLabel countryLabel = new JLabel("Country:");
        currentCountryField = new JTextField();
        JLabel provinceLabel = new JLabel("Province:");
        currentProvinceField = new JTextField();
        JLabel districtLabel = new JLabel("District:");
        currentDistrictField = new JTextField();
        JLabel sectorLabel = new JLabel("Sector:");
        currentSectorField = new JTextField();
        JLabel cellLabel = new JLabel("Cell:");
        currentCellField = new JTextField();
        JLabel villageLabel = new JLabel("Village:");
        currentVillageField = new JTextField();

        currentLocationPanel.add(countryLabel);
        currentLocationPanel.add(currentCountryField);
        currentLocationPanel.add(provinceLabel);
        currentLocationPanel.add(currentProvinceField);
        currentLocationPanel.add(districtLabel);
        currentLocationPanel.add(currentDistrictField);
        currentLocationPanel.add(sectorLabel);
        currentLocationPanel.add(currentSectorField);
        currentLocationPanel.add(cellLabel);
        currentLocationPanel.add(currentCellField);
        currentLocationPanel.add(villageLabel);
        currentLocationPanel.add(currentVillageField);

        JButton nextButton = new JButton("Next");
        nextButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                showEducationWindow();
            }
        });
        currentLocationPanel.add(nextButton);

        currentPanel = currentLocationPanel;
        add(currentPanel);

        revalidate();
    }

    private void showEducationWindow() {
        getContentPane().removeAll();
        revalidate();
        repaint();

        // Fourth window: Education Background
        JPanel educationPanel = new JPanel(new GridLayout(5, 2, 10, 10));
        JLabel educationLabel = new JLabel("Education Background:");
        educationField = new JTextField();
        educationPanel.add(educationLabel);
        educationPanel.add(educationField);

        JLabel currentSchoolLabel = new JLabel("Current School:");
        currentSchoolField = new JTextField();
        educationPanel.add(currentSchoolLabel);
        educationPanel.add(currentSchoolField);

        JLabel nextSchoolLabel = new JLabel("Next School Option 1:");
        String[] schoolOptions = {"Option 1", "Option 2", "Option 3"};
        nextSchool1ComboBox = new JComboBox<>(schoolOptions);
        educationPanel.add(nextSchoolLabel);
        educationPanel.add(nextSchool1ComboBox);

        nextSchoolLabel = new JLabel("Next School Option 2:");
        nextSchool2ComboBox = new JComboBox<>(schoolOptions);
        educationPanel.add(nextSchoolLabel);
        educationPanel.add(nextSchool2ComboBox);

        nextSchoolLabel = new JLabel("Next School Option 3:");
        nextSchool3ComboBox = new JComboBox<>(schoolOptions);
        educationPanel.add(nextSchoolLabel);
        educationPanel.add(nextSchool3ComboBox);

        JButton nextButton = new JButton("Next");
        nextButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                showParentsWindow();
            }
        });
        educationPanel.add(nextButton);

        currentPanel = educationPanel;
        add(currentPanel);

        revalidate();
    }

    private void showParentsWindow() {
        getContentPane().removeAll();
        revalidate();
        repaint();

        // Fifth window: Parents' Names
        JPanel parentsPanel = new JPanel(new GridLayout(4, 2, 10, 10));
        JLabel motherNameLabel = new JLabel("Mother's Name:");
        motherNameField = new JTextField();
        JLabel fatherNameLabel = new JLabel("Father's Name:");
        fatherNameField = new JTextField();
        JLabel otherGuardianLabel = new JLabel("Other Guardian's Name:");
        otherGuardianField = new JTextField();
        parentsPanel.add(motherNameLabel);
        parentsPanel.add(motherNameField);
        parentsPanel.add(fatherNameLabel);
        parentsPanel.add(fatherNameField);
        parentsPanel.add(otherGuardianLabel);
        parentsPanel.add(otherGuardianField);

        JButton nextButton = new JButton("Next");
        nextButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                showDisabilitiesWindow();
            }
        });
        parentsPanel.add(nextButton);

        currentPanel = parentsPanel;
        add(currentPanel);

        revalidate();
    }

    private void showDisabilitiesWindow() {
        getContentPane().removeAll();
        revalidate();
        repaint();

        // Sixth window: Disabilities or Colonial Diseases
        JPanel disabilitiesPanel = new JPanel(new GridLayout(5, 1, 10, 10));

        disabilitiesCheckBox = new JCheckBox("Disability");
        colonialDiseaseCheckBox = new JCheckBox("Colonial Disease");

        disabilitiesPanel.add(disabilitiesCheckBox);
        disabilitiesPanel.add(colonialDiseaseCheckBox);

        disabilityArea = new JTextArea();
        disabilityArea.setBorder(BorderFactory.createTitledBorder("Explain Disability"));
        disabilityArea.setLineWrap(true);
        disabilityArea.setWrapStyleWord(true);

        colonialDiseaseArea = new JTextArea();
        colonialDiseaseArea.setBorder(BorderFactory.createTitledBorder("Explain Colonial Disease"));
        colonialDiseaseArea.setLineWrap(true);
        colonialDiseaseArea.setWrapStyleWord(true);

        disabilitiesPanel.add(disabilityArea);
        disabilitiesPanel.add(colonialDiseaseArea);

        JButton submitButton = new JButton("Submit");
        submitButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                submitForm();
            }
        });
        disabilitiesPanel.add(submitButton);

        currentPanel = disabilitiesPanel;
        add(currentPanel);

        revalidate();
    }

    private void submitForm() {
        String firstName = firstNameField.getText();
        String middleName = middleNameField.getText();
        String lastName = lastNameField.getText();
        String nid = nidField != null ? nidField.getText() : "";
        String dob = yearComboBox.getSelectedItem() + "-" + String.format("%02d", monthComboBox.getSelectedItem()) + "-" + String.format("%02d", dayComboBox.getSelectedItem());
        String gender = (String) genderComboBox.getSelectedItem();
        String education = educationField.getText();
        String currentSchool = currentSchoolField.getText();
        String nextSchool1 = (String) nextSchool1ComboBox.getSelectedItem();
        String nextSchool2 = (String) nextSchool2ComboBox.getSelectedItem();
        String nextSchool3 = (String) nextSchool3ComboBox.getSelectedItem();
        String motherName = motherNameField.getText();
        String fatherName = fatherNameField.getText();
        String otherGuardian = otherGuardianField.getText();
        String disability = disabilitiesCheckBox.isSelected() ? disabilityArea.getText() : "";
        String colonialDisease = colonialDiseaseCheckBox.isSelected() ? colonialDiseaseArea.getText() : "";

        String birthPlace = String.format("%s, %s, %s, %s, %s, %s",
                birthCountryField.getText(), birthProvinceField.getText(), birthDistrictField.getText(),
                birthSectorField.getText(), birthCellField.getText(), birthVillageField.getText());
        String currentPlace = String.format("%s, %s, %s, %s, %s, %s",
                currentCountryField.getText(), currentProvinceField.getText(), currentDistrictField.getText(),
                currentSectorField.getText(), currentCellField.getText(), currentVillageField.getText());

        // Processing the collected data (for demonstration, just print it)
        StringBuilder data = new StringBuilder();
        data.append("First Name: ").append(firstName).append("\n");
        if (!middleName.isEmpty()) {
            data.append("Middle Name: ").append(middleName).append("\n");
        }
        data.append("Last Name: ").append(lastName).append("\n");
        if (!nid.isEmpty()) {
            data.append("National ID Number: ").append(nid).append("\n");
        }
        data.append("Date of Birth: ").append(dob).append("\n");
        data.append("Gender: ").append(gender).append("\n");
        data.append("Education Background: ").append(education).append("\n");
        data.append("Current School: ").append(currentSchool).append("\n");
        data.append("Next School Option 1: ").append(nextSchool1).append("\n");
        data.append("Next School Option 2: ").append(nextSchool2).append("\n");
        data.append("Next School Option 3: ").append(nextSchool3).append("\n");
        data.append("Mother's Name: ").append(motherName).append("\n");
        data.append("Father's Name: ").append(fatherName).append("\n");
        data.append("Other Guardian's Name: ").append(otherGuardian).append("\n");

        if (!disability.isEmpty()) {
            data.append("Disability: ").append(disability).append("\n");
        }
        if (!colonialDisease.isEmpty()) {
            data.append("Colonial Disease: ").append(colonialDisease).append("\n");
        }

        data.append("Birth Place: ").append(birthPlace).append("\n");
        data.append("Current Location: ").append(currentPlace).append("\n");

        // Displaying the collected data
        JOptionPane.showMessageDialog(this, data.toString(), "Registration Details", JOptionPane.INFORMATION_MESSAGE);

        // Optionally, you could save the data to a file or database
    }

    private Integer[] getYearArray() {
        Integer[] years = new Integer[101];
        int currentYear = java.util.Calendar.getInstance().get(java.util.Calendar.YEAR);
        for (int i = 0; i < 101; i++) {
            years[i] = currentYear - i;
        }
        return years;
    }

    private Integer[] getMonthArray() {
        Integer[] months = new Integer[12];
        for (int i = 0; i < 12; i++) {
            months[i] = i + 1;
        }
        return months;
    }

    private Integer[] getDayArray(int maxDay) {
        Integer[] days = new Integer[maxDay];
        for (int i = 0; i < maxDay; i++) {
            days[i] = i + 1;
        }
        return days;
    }

    private int getMaxDay(int month) {
        if (month == 2) {
            int year = (int) yearComboBox.getSelectedItem();
            if (year % 4 == 0 && (year % 100 != 0 || year % 400 == 0)) {
                return 29; // leap year
            } else {
                return 28;
            }
        } else if (month == 4 || month == 6 || month == 9 || month == 11) {
            return 30;
        } else {
            return 31;
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new SchoolRegistrationForm();
            }
        });
    }
}

