cadastro-pessoa-swing/
│
├── README.md
│
└── src/
    └── view/
        └── CadastroPessoa.java

package view;

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class CadastroPessoa extends JFrame {

    private JTextField txtNome, txtCpf, txtEndereco, txtTelefone, txtEmail;
    private JComboBox<String> cbSexo, cbEstadoCivil;
    private JTextArea txtObservacoes;
    private JButton btnGravar, btnCancelar, btnVoltar;

    public CadastroPessoa() {
        super("Cadastro de Pessoa");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(650, 500);
        setLocationRelativeTo(null);
        setResizable(false);

        setLayout(new GridBagLayout());
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(5, 5, 5, 5);
        gbc.fill = GridBagConstraints.HORIZONTAL;

        // ======= Título =======
        JLabel lblTitulo = new JLabel("Preencha os dados corretamente e clique em Gravar Dados");
        lblTitulo.setFont(new Font("Arial", Font.BOLD, 14));
        gbc.gridx = 0;
        gbc.gridy = 0;
        gbc.gridwidth = 4;
        add(lblTitulo, gbc);
        gbc.gridwidth = 1;

        // ======= Nome =======
        gbc.gridy++;
        gbc.gridx = 0;
        add(new JLabel("Nome Completo:"), gbc);
        txtNome = new JTextField(25);
        gbc.gridx = 1;
        gbc.gridwidth = 3;
        add(txtNome, gbc);
        gbc.gridwidth = 1;

        // ======= CPF =======
        gbc.gridy++;
        gbc.gridx = 0;
        add(new JLabel("CPF:"), gbc);
        txtCpf = new JTextField(15);
        gbc.gridx = 1;
        gbc.gridwidth = 3;
        add(txtCpf, gbc);
        gbc.gridwidth = 1;

        // ======= Endereço =======
        gbc.gridy++;
        gbc.gridx = 0;
        add(new JLabel("Endereço:"), gbc);
        txtEndereco = new JTextField(25);
        gbc.gridx = 1;
        gbc.gridwidth = 3;
        add(txtEndereco, gbc);
        gbc.gridwidth = 1;

        // ======= Telefone =======
        gbc.gridy++;
        gbc.gridx = 0;
        add(new JLabel("Telefone:"), gbc);
        txtTelefone = new JTextField(15);
        gbc.gridx = 1;
        gbc.gridwidth = 3;
        add(txtTelefone, gbc);
        gbc.gridwidth = 1;

        // ======= E-mail =======
        gbc.gridy++;
        gbc.gridx = 0;
        add(new JLabel("E-mail:"), gbc);
        txtEmail = new JTextField(25);
        gbc.gridx = 1;
        gbc.gridwidth = 3;
        add(txtEmail, gbc);
        gbc.gridwidth = 1;

        // ======= Sexo =======
        gbc.gridy++;
        gbc.gridx = 0;
        add(new JLabel("Sexo:"), gbc);
        String[] sexos = {"Selecione", "Masculino", "Feminino", "Outro"};
        cbSexo = new JComboBox<>(sexos);
        gbc.gridx = 1;
        gbc.gridwidth = 3;
        add(cbSexo, gbc);
        gbc.gridwidth = 1;

        // ======= Estado Civil =======
        gbc.gridy++;
        gbc.gridx = 0;
        add(new JLabel("Estado Civil:"), gbc);
        String[] estadosCivis = {"Selecione", "Solteiro(a)", "Casado(a)", "Divorciado(a)", "Viúvo(a)"};
        cbEstadoCivil = new JComboBox<>(estadosCivis);
        gbc.gridx = 1;
        gbc.gridwidth = 3;
        add(cbEstadoCivil, gbc);
        gbc.gridwidth = 1;

        // ======= Observações =======
        gbc.gridy++;
        gbc.gridx = 0;
        gbc.anchor = GridBagConstraints.NORTH;
        add(new JLabel("Observações:"), gbc);
        txtObservacoes = new JTextArea(4, 25);
        JScrollPane scroll = new JScrollPane(txtObservacoes);
        gbc.gridx = 1;
        gbc.gridwidth = 3;
        gbc.fill = GridBagConstraints.BOTH;
        add(scroll, gbc);
        gbc.gridwidth = 1;
        gbc.fill = GridBagConstraints.HORIZONTAL;
        gbc.anchor = GridBagConstraints.CENTER;

        // ======= Botões =======
        gbc.gridy++;
        gbc.gridx = 0;
        btnGravar = new JButton("Gravar Dados");
        btnCancelar = new JButton("Cancelar Cadastro");
        btnVoltar = new JButton("Voltar");

        JPanel panelBotoes = new JPanel(new FlowLayout(FlowLayout.CENTER, 15, 0));
        panelBotoes.add(btnGravar);
        panelBotoes.add(btnCancelar);
        panelBotoes.add(btnVoltar);

        gbc.gridwidth = 4;
        add(panelBotoes, gbc);

        // ======= Ações =======
        btnGravar.addActionListener(e -> validarCampos());
        btnCancelar.addActionListener(e -> limparCampos());
        btnVoltar.addActionListener(e -> System.exit(0));
    }

    private void validarCampos() {
        if (txtNome.getText().trim().isEmpty()) {
            mostrarErro("Preencha o campo Nome Completo.");
        } else if (txtCpf.getText().trim().isEmpty()) {
            mostrarErro("Preencha o campo CPF.");
        } else if (txtEndereco.getText().trim().isEmpty()) {
            mostrarErro("Preencha o campo Endereço.");
        } else if (txtTelefone.getText().trim().isEmpty()) {
            mostrarErro("Preencha o campo Telefone.");
        } else if (txtEmail.getText().trim().isEmpty()) {
            mostrarErro("Preencha o campo E-mail.");
        } else if (cbSexo.getSelectedIndex() == 0) {
            mostrarErro("Selecione o Sexo.");
        } else if (cbEstadoCivil.getSelectedIndex() == 0) {
            mostrarErro("Selecione o Estado Civil.");
        } else if (txtObservacoes.getText().trim().isEmpty()) {
            mostrarErro("Preencha o campo Observações.");
        } else {
            JOptionPane.showMessageDialog(this, "✅ Dados gravados com sucesso!");
        }
    }

    private void mostrarErro(String mensagem) {
        JOptionPane.showMessageDialog(this, mensagem, "Erro de Validação", JOptionPane.ERROR_MESSAGE);
    }

    private void limparCampos() {
        txtNome.setText("");
        txtCpf.setText("");
        txtEndereco.setText("");
        txtTelefone.setText("");
        txtEmail.setText("");
        cbSexo.setSelectedIndex(0);
        cbEstadoCivil.setSelectedIndex(0);
        txtObservacoes.setText("");
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new CadastroPessoa().setVisible(true));
    }
}
